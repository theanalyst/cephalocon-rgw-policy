<!-- .slide: data-state="cover" id="cover-page" data-timing="20" -->
<div class="title">
    <h1>Releasing Krakens & other Cephalopods in the Wild</h1>
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
<h1>Ceph: through the years</h1>
</div>


<!-- .slide: data-state="normal" id="history" data menu title="history"-->
# History
- Started off with Sage's PhD thesis
- Research grant from Dept. of Energy in cooperation with 
  Los Alamos, Lawrence Livermore & National Labs
<img data-src="images/old_ceph_logo.png",
     style="float: right"
     alt="old ceph logo">
- Code hit the CVS repository in 2004 (15th year in running!)
- Open Sourced in 2006 under LGPLv2*
- Research phase 2004 -2007, DH 2007-2012, Inktank 2012-14


<!-- .slide: data-state="normal" id="history" data menu title="history"-->
<img alt="authors" width=95% data-src="images/author-org.svg"/>


<!-- .slide: data-state="normal" id="timeline" data menu title="timeline"-->

# Timeline of Major features
- Object classes 2009 
- Librados 2009
- Radosgw 2009
- cephx 2009
- kernel cephfs 2010
- RBD 2010
- kRBD 2011
- Argonaut v0.48 Jul 2012



<!-- .slide: data-state="section-break" data-menu-title="release policy" id="release policy" -->
<div class="title">
<h1> Release Policy </h1>
<h2> The Past, Present and Future </h2>
</div>


<!-- .slide: data-state="normal" id="naming policy" data menu title="naming policy"-->

* Naming Policy: Alphabetical release names, usually after a cephalopod
  
<img alt="argonaut", src="images/argonaut.png" width=22% />
<img alt="bobtail", src="images/bobtail.png" width=22% />
<img alt="cuttlefish", src="images/cuttlefish.png" width=22% />
<img alt="dumpling", src="images/dumpling.png" width=22% />
<img alt="firefly", src="images/Firefly.png" width=22% />
<img alt="giant", src="images/giant.png" width=22% />
<img alt="hammer", src="images/hammer.png" width=22% />
<img alt="infernalis", src="images/infernalis.png" width=22% />
<img alt="jewel", src="images/jewel.png" width=22% />
<img alt="kraken", src="images/kraken.png" width=22% />
<img alt="luminous", src="images/luminous.png" width=22% />
<img alt="mimic", src="images/mimic.png" width=22% />
<img alt="nautilus", src="images/nautilus.png" width=22% align="middle" />


<!-- .slide: data-state="normal" id="release-policy-past" data menu title="release-policy-past"-->
# Version numbering: Past 
+ Until hammer, major releases did not have a fixed scheme
+ More or less random numbers for major releases 0.48 (argonaut), 0.56 (bobtail)
+ Minor versions represented backport versions eg.
```
    firefly (v0.80) v0.80.1 → v0.80.11
    hammer (v0.94)  v0.94.1 → v0.94.10
```
+ Approximate 6 month release cadence until Firefly May '14


<!-- .slide: data-state="normal" id="version-present" data menu title="version-present"-->
# Version numbering: Present
- Version number transition from Hammer v0.94 to Infernalis v9.2.0
- New scheme `x.y.z`
  + x: major release number
  + y: 0 - dev. 1 - RC 2 - stable*
  + z: point release number 
- Also readable from the version string / ceph versions command  
  ```
  ceph version 14.2.1-62-g584940cd0f (584940cd0f9c76aa3a91b525dbd00b81166c1778) nautilus (stable)
  ```  
- Each major release gets the next successive number & letter
  + Infernalis 9.y.z ...
  + Luminous 12.y.z
  + Mimic 13.y.z
  + Nautilus 14.y.z
  + Octopus 15.y.z (currently in development)


<!-- .slide: data-state="normal" id="release-past" data menu title="release-past"-->
# Release Cadence: Past 
- From Firefly until Luminous, even numbered releases were LTS
  + Backports and bug fixes until the next LTS releases
  + Some releases received a lot of backports firely 11, Hammer 10, Luminous 12+
- odd numbered releases eg Kraken, got less attention and were not maintained for a long time 
  + EOL'ed when the next release was declared stable
  + Backports only for a single release timeframe


<!-- .slide: data-state="normal" id="release-present" data menu title="release-present"-->
# Release Cadence: Present
- New release cadence as of Luminous:
+ 9 month release time
+ at any given time, at least 2 stable releases maintained 
+ These will receive backports and new releases from time to time 
- 3 categories of releases: dev, RC, stable


<!-- .slide: data-state="normal" id="dev-releases" data menu title="dev-release"-->
## Release Type: Development releases
- Every ~6-8 weeks towards the later end of release cycle
- Intended only for testing 
- Upgrade tests from the last stable release
- Shaman builds
- Upgradeability between dev releases
  + Efforts are made to allow *offline* upgrade 
  + No real attempts to support rolling upgrades 
  + intent: deployment of non-prod. clusters without the need to repopulate data 


<!-- .slide: data-state="normal" id="rc" data menu title="rc"-->
## Release Type: Release Candidates

- Feature release ~6 weeks prior to the stable rleease
- Focus mainly on bug fixes after this point
- Intended for testing and validation of upcoming stable release
- *NOT* meant for production 


<!-- .slide: data-state="normal" id="stable" data menu title="stable"-->
## Release Type: Stable Releases

- Initial release will be `x.2.0`
- Semi regular bug fixes and occasional small feature backports
- Intended for production deployments
- Backport support for 2 full release cycles
- Online rolling upgrade support & testing from the last 2 stable releases 
  (starting from Luminous)


<!-- .slide: data-state="normal" id="upgrades" data menu title="upgrades"-->
# Upgrade support
- Online rolling upgrade support & testing from the last 2 stable releases
- Ie. for Nautilus this means:
  + Luminous (eg. v12.2.10) → Nautilus (eg. 14.2.1)
  + Mimic → Nautilus
- For releases older than these, LTS upgrades were supported
  + Jewel → Kraken → Luminous 
  + Jewel → Luminous 
- Odd releases must reach prior to Luminous must reach Luminous before upgrade
  + ~~Kraken → Mimic~~
  + Kraken → Luminous → Mimic 


<!-- .slide: data-state="normal" id="upgrade-notes" data menu title="upgrade-notes"-->
# Upgrade Notes
- Usually at every major release announcement a special section mentioned for
  upgrade notes
- These precautions are to be followed when upgrading from the previous stable
  release point to current stable release point 
- While skipping versions, it is best to go through the release notes of
  previous sections for special precautions



<!-- .slide: data-state="section-break" data-menu-title="Workflow" id="Workflow" -->
<div class="title">
<h1>Workflow</h1>
<h2>How to Contribute</h2>
</div>


<!-- .slide: data-state="normal" id="feature prs" data menu title="feature-prs"-->
# Workflow
## Feature PRs
- Starts with mail to ceph-devel &/ tracker issue
- Always PRs against master
  + Apply labels if you have permissions, these are used in release notes
  + Titling the PR correcly also helps in release notes

- Signed-Off-By:
  + Jenkins checked, needed for acceptance
  + Sign with organizational email/ add mailmap entries to map credits to organization
  + unknown affiliations may be marked as individual contributors with no organization

- Backports of features are generally avoided* 
  - unless the functionality is really important & aids bug fixes

- Testing usually done in batches, as teuthology runs are expensive in terms of
  resources & time


<!-- .slide: data-state="normal" id="bug-fix" data menu title="bug fix prs"-->
## Bug Reports & Fixes
- Always mark the release affected while raising a bug
  + Helps us mark the relevant backports when addressing the bug fix
  + Developer raising the fix against master may not be the backporter
  
- Bug scrubs occur weekly in every component
  + Consider joining, get an overview of major bugs affecting a release
  + Many "easy-first-bugs" are also found, with lower barrier of entry
  
- When the master PR is merged, the developer/reviewer must ensure
  + status moves to "Pending Backport"
  + Backport fields are appropriately filled
