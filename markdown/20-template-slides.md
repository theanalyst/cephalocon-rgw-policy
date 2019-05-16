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
  + y: 0 - dev. 1 - RC 2 - stable
  + z: point release number 
- Each major release gets the next successive number & letter
  + ~~infernalis 9.y.z~~
  + ~~Jewel 10.y.z~~
  + ~~Kraken 11.y.z~~
  + Luminous 12.y.z
  + Mimic 13.y.z
  + Nautilus 14.y.z
  + Octopus 15.y.z (currently in development)


<!-- .slide: data-state="normal" id="release-past" data menu title="release-past"-->
# Release Cadence: Past 
- From Firefly until Luminous, even numbered releases were LTS
  + Backports and bug fixes until the next LTS releases
- odd numbered releases eg Kraken, got less attention and were not maintained for a long time 
  + EOL'ed when the next release was declared stable
  + Backports only for a single release timeframe

<!-- .slide: data-state="normal" id="release-present" data menu title="release-present"-->
# Release Cadence: Present
- New release cadence as of Luminous:
  + 9 month release time
  + at any given time, at least 2 stable releases maintained (receiving backports and new releases from time to time )
