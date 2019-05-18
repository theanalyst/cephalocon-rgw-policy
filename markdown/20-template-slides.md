<!-- .slide: data-state="cover" id="cover-page" -->
<div class="title">
    <h1>Avoiding the Curious Case of Leaky Cauldrons</h1>
        <h2>Access Control done right!</h2>
</div>

<div class="row presenters">
    <div class="presenter presenter-1">
        <h3 class="name">Abhishek Lekshmanan</h3>
        <h3 class="job-title">Senior Software Developer</h3>
        <h3 class="email"><a href="mailto:abhishek@suse.com">abhishek@suse.com</a></h3>
    </div>
</div>



<!-- .slide: data-state="section-break" data-menu-title="history-title" id="history-title" -->
<div class="title">
<h1>RGW: Overview</h1>
</div>


<!-- .slide: data-state="normal" id="intro" data menu title="intro"-->
# RGW
- Object Storage Client to the Ceph Cluster
- Exposes S3 & Swift API 
- Immutable Objects*, not 1:1 mapped to rados objects
- User Accounts, Buckets, ACLs
- Rich ecosystem of S3 & Swift client tooling which can be leveraged


<!-- .slide: data-state="normal" id="use-cases" data menu title="use-cases"-->
# Typical Use Cases
- Cloud Native application data
- CDN usecases
- Backup & Archival 
- DR (with multisite)


<!-- .slide: data-state="normal" id="fundamentals" data menu title="fundamentals"-->
# Fundamentals
- Users
- Buckets
- Keys



<!-- .slide: data-state="section-break" data-menu-title="data-sharing" id="data-sharing" -->
<div class="title">
<h1>Controlling Access: S3 API</h1>
</div>


<!-- .slide: data-state="normal" id="share-overview" data menu title="share-overview"-->
# Controlling Access: S3 API
- ACLs
- Bucket Policy
- User Policy


<!-- .slide: data-state="normal" id="acl-overview" data menu title="acl-overview"-->
# ACLs 
## Overview
- Available for the following resources 
  + Bucket ACLs
  + Object ACLs
- Default ACL always created with private and owner full control permissions
- Two types
  + Normal ACL: specified with one of the specific PUT ACL ops
  + Canned ACL: specified inline during an op


<!-- .slide: data-state="normal" id="normal-acls" data menu title="normal-acls"-->

## Normal ACLs
Syntax

```xml
<AccessControlPolicy xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
  <Owner>
    <ID>*** Owner-Canonical-User-ID ***</ID>
    <DisplayName>owner-display-name</DisplayName>
  </Owner>
  <AccessControlList>
    <Grant>
      <Grantee type="Canonical User">
        <ID>*** Owner-Canonical-User-ID ***</ID>
        <DisplayName>display-name</DisplayName>
      </Grantee>
      <Permission>FULL_CONTROL</Permission>
    </Grant>
  </AccessControlList>
</AccessControlPolicy> 
```


<!-- .slide: data-state="normal" id="normal-acls elt" data menu title="normal-acls elt"-->

### Elements
- Owner
  + Usually Bucket owner, but maybe uploader
  + Always has `FULL_CONTROL` of the bucket
  + trying to change this will be a noop
  
- Grantee
  + User
    - specified by `tenant_id:user_id` 
  + Group
    - All Users Group
	  + Public 
    - Authenticated Users Group
	  + Remember Authenticated not Authorized


- Permissions
  + `READ`
  + `WRITE`
  + `READ_ACP`
  + `WRITE_ACP`
  + `FULL_CONTROL`


<!-- .slide: data-state="normal" id="canned-acls" data menu title="canned-acls"-->
### Canned ACLs
+ private
+ bucket-owner-read
+ bucket-owner-full-control
+ public-read
+ public-read-write


<!-- .slide: data-state="normal" id="example1" data menu title="example1"-->
## Example Use Case
Case 1: public folder within a bucket

A bucket has a folder public whose contents need to be
publically accessible 
+ <p class="fragment fade-in-then-out">Obviously make the bucket public</p>
+ <p class="fragment">Copy public contents to another public bucket</p>
+ <p class="fragment">Set object ACL to public for each of the objects in public folder</p>
<p class="fragment">  - More secure than the other options, but new objects need to be taken care of</p>
<p class="fragment">  - Turning this off requires effort</p>


<!-- .slide: data-state="normal" id="example2" data menu title="example2"-->
## Example Use Cases
- Case 2: Simple Upload only shared bucket
  + Alice has a bucket `testbucket`, wants to make Bob upload keys to it
  + Bucket created, with `WRITE` acl to Bob
  ```json
        {
            "Grantee": {
                "Type": "CanonicalUser",
                "ID": "Bob"
            },
            "Permission": "WRITE"
        }
  ```
  + Bob writes a simple object `octocat.jpg` to `testbucket`
  + <p class="fragment">Object created with default acl</p> 
  + <p class="fragment">Default ACL with respect to Object Owner & not Bucket Owner</p>
  + <p class="fragment">
  ```
  {
    "Owner": {"DisplayName": "Bobby","ID": "bob"},
    "Grants": [{"Grantee": {
                "Type": "CanonicalUser",
                "DisplayName": "Bobby",
                "ID": "bob"},
            "Permission": "FULL_CONTROL"}]}
	```
</p>


<!-- .slide: data-state="normal" id="examples-ans" data menu title="examples-ans"-->
- Case2: Solutions To actually make Alice access `octocat`
  + <p class="fragment highlight-red">Upload with public read ACL</p>
  + <p class="fragment">add Alice as a grantee with READ as object acl</p>
  + <p class="fragment">Use the bucket-owner-read/full-control canned acl</p>
  + <p class="fragment">Note, this cannot be enforced with ACLs yet</p>


<!-- .slide: data-state="normal" id="acl-issues" data menu title="acl-issues"-->
### Issues
- Blanket Permissions
- Not possible to provide access to grantee based on attributes on object
  + Object tags/x-amz-attributes
- Not possible to enforce grantee to follow certain attributes when writing
  + For eg. Encrypted uploads-only
- Public ACLs are too risky other than in specific circumstances


<!-- .slide: data-state="normal" id="bucket-policy" data menu title="bucket-policy"-->
# Bucket Policy
+ Grant access to resources (buckets, objects)
+ Richer policy based language

```json
{
  "Version":"2012-10-17",
  "Statement":[
    {
      "Sid":"PublicReadformyOrg",
      "Effect":"Allow",
      "Principal": "*",
      "Action":["s3:GetObject"],
      "Resource":["arn:aws:s3:::examplebucket/*"]
       "Condition": {
         "IpAddress": {"aws:SourceIp": "54.240.143.0/24"},
    }
  ]
}
```


<!-- .slide: data-state="normal" id="bucket-lang" data menu title="bucket-lang"-->
## Language Overview
- Principal
- Action 
- Effect - Allow/Deny
- Resource
- Condition


<!-- .slide: data-state="normal" id="principal" data menu title="principal"-->
### Principal
```
"AWS":"Account-ARN"
```
+ Grantee
+ TenantID:UserID in RGW context


<!-- .slide: data-state="normal" id="resource" data menu title="resource"-->
### Resource

Syntax
```
arn:partition:service:region:namespace:relative-id
```

- Not everything needs to be specified 
- Usually a bucket/objects
- Wildcards 
  `*` Any
  `?` single char

Example:
```
arn:aws:s3:::bucket_name
arn:aws:s3:::bucket_name/key_name

```


<!-- .slide: data-state="normal" id="action" data menu title="action"-->

### Condition
- Policy is evaluated to True only when condition is satisfied
- Two types of conditional: AWS wide keys, S3 specific
  + We don't support the full AWS Subset, but still support a very large subset
	aws:Username, aws:SourceIp, aws:SecureTransport etc.
  + S3 specific keys: specific conditionals depending on the API
  + eg. createBucket, s3:x-amz-acl and s3:x-amz-grant-<perm> can be specified
        ListBucket, s3:prefix 
        PutObject, s3:x-amz-server-side-encryption
		
	also restrict based on presence of specific object tags


<!-- .slide: data-state="normal" id="policy-review" data menu title="policy-review"-->
## Adding it all up
### Case 1: Partially public bucket
Expose only a folder in a bucket

```
                {...
                   "Effect": "Allow",
                    "Principal": {"AWS": "*"},
                    "Action": "s3:ListBucket",
                    "Resource": "arn:aws:s3:::s3testb",
                    "Condition": {
                        "StringEquals" : {"s3:prefix": "public"}}
                },
                {...
                    "Principal": {"AWS": "*"},
                    "Action": "s3:GetObject",
                    "Resource": "arn:aws:s3:::s3testb/public*"
                }

```

- Ability to List the bucket with the prefix also can be allowed in
  addition to GETs
- Dropping the policy will revert back to the private mode


<!-- .slide: data-state="normal" id="policy-case2" data menu title="policy-case2"-->
### Case 2: Alice's write-only shared bucket
```
	{..
	"Action": "s3:PutObject",
	"Resource": "arn:aws:s3:::s3testb/bob*"
	"Condition": {
		"StringEquals" : {
            "s3:x-amz-acl": "bucket-owner-full-control"
			}
	}..	
```
Can additionally impose
- path restictions
- Object tag/ metadata restrictions 
- Read/Write/List permissions 
- Encryption
...
