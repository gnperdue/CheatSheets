## New SVN Repo

#### Tested

    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/docs docs
    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/trunk trunk
    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_9_0 R-2_9_0
    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_10_0 R-2_10_0
    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_10_2 R-2_10_2
    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_10_4 R-2_10_4
    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/devel/branches/mec_devel mec_devel
    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/devel/branches/resupdates resupdates
    svn co --quiet http://genie.hepforge.org/svn/generator/branches/R-2_9_0 R-2_9_0
    svn co --quiet http://genie.hepforge.org/svn/generator/trunk trunk
    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/comparisons/trunk comparisons_trunk

    svn copy -m "start 2.8.6 REDTOP devel" \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_8_6 \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/devel/branches/Redtop-2_8_6

    svn copy -m "MEC devel" \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/trunk \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/devel/branches/mec_devel

    svn copy -m "DIS Re-eval" \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/trunk \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/devel/branches/dis_reeval

    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/devel/branches/Redtop-2_8_6 Redtop-2_8_6
    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/devel/branches/mec_devel mec_devel

    svn export svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/devel/branches/honda_flux-trunk_rv5318 honda
    svn export svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_9_0 R-2_9_0_export
    svn export svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_10_0 GENIE-Generator_v2.10.0
    svn export svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_10_2 GENIE-Generator_v2.10.2
    svn export svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_10_2 GENIE
    svn export svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_10_4 GENIE
    svn export svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/trunk trunk

    svn move -m "rename branch for S. Dytman" \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/devel/branches/newfsi \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/devel/branches/spectral_func_vt
      
    svn copy -m "GENIE 2.10.0" \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_9_0 \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_10_0

    svn copy -m "GENIE 2.10.2" \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_10_0 \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_10_2

    # merge trunk into the branch I'm working in...
    svn merge svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/trunk

    # merge another (devel) branch into the branch I'm working in...
    svn merge svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/devel/branches/mec_devel

    # diffs over a range of commits
    svn diff --summarize -r5547:5681 svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_10_2

    # look at the logs over a range
    svn log -r5547:5681 data/logo/genie_banner_long.txt 

#### Untested

    svn copy -m "start 2.9.0 REDTOP devel" \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/branches/R-2_9_0 \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/generator/devel/branches/Redtop-2_9_0

#### Misc

Post-commit hooks:

    gnperdue@login:/hepforge/svn/genie/hooks$ more post-commit
    #!/bin/sh
    REPOS="$1"
    REV="$2"

    /usr/share/subversion/hook-scripts/commit-email.pl \
      "$REPOS" "$REV" perdue@fnal.gov



## Old SVN Repo

    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/branches/R-2_8_4 R-2_8_4
    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/branches/R-2_8_6 R-2_8_6

    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/branches/R-2_9_0 R-2_9_0
    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/trunk trunk

    svn co --quiet http://genie.hepforge.org/svn/branches/R-2_9_0 R-2_9_0

    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/branches/_devel_branch_not_for_users_01may13_sd_hj3ga7sk2va8q newhafsi

    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/branches/_devel_branch_not_for_users_v280_06jun13_hugh_nd9832nxll3a1 bscohpi

    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/devel/branches/miniboone_fits tuning_and_fits

    svn list http://genie.hepforge.org/svn/branches 

    svn export http://genie.hepforge.org/svn/branches/R-2_8_4 Genie-2.8.4
    svn export http://genie.hepforge.org/svn/branches/R-2_8_6 GENIE_2_8_6
    svn export http://genie.hepforge.org/svn/branches/R-2_9_0 GENIE_2_9_0
    tar -czvf Genie-2.8.4.tar.gz Genie-2.8.4/
    svn export http://genie.hepforge.org/svn/trunk trunk
    svn export svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/branches/R-2_9_0 R-2_9_0

    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/docs docs

    svn co svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/docs/policy/bylaws bylaws

    svn export svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/docs/manuals genie-manuals

    svn copy -m "start R-2_8_6" \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/branches/R-2_8_4 \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/branches/R-2_8_6

    svn copy -m "start R-2_9_0" \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/branches/R-2_8_6 \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/branches/R-2_9_0

    svn copy -m "start a new trunk" \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/branches/R-2_9_0 \
      svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/trunk

    svn diff svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/trunk svn+ssh://gnperdue@svn.hepforge.org/hepforge/svn/genie/branches/R-2_9_0
