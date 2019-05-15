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


<!-- .slide: data-state="normal" id="release-policy-past" data menu title="release-policy-past"-->

- Alphabetical release names, Argonaut -> Nautilus, Octopus 
- Version numbering: Past 
  + Until hammer, major releases did not have a fixed scheme
  + More or less random numbers 0.48 (argonaut), 0.56 (bobtail)
  + Minor versions represented backport versions eg.
        firefly (v0.80) v0.80.1-> v0.80.11)
        hammer (v0.94)  v0.94.1 -> v0.94.10
  + Approximate 6 month release cadence until Firefly May '14

  
