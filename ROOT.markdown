Histograms
----------

    // Get better color palette.
    gStyle->SetPalette(1);
    
    // Command line rebin
    h1->Rebin(); // by 2
    h1->Rebin(5); // by 5
    
    // Set background color to white
    'Canvas 1'->SetFillColor(kWhite);


Chains
------

    TChain ch("ch","ch")                   
    ch->Add("SIM_minerva_00000513*.root/CCInclusiveReco",0)

    TChain ch("ch","ch");
    ch->Add("02/SIM_minerva_00000002_Subruns_*.root/RecoTracks",0)
    ch->Add("04/SIM_minerva_00000004_Subruns_*.root/RecoTracks",0)
    ch.MakeClass("RecoTracks")



Trees
-----

    TFile *_file0 = TFile::Open("/minerva/data/users/perdue/mc_production/nogrid/minerva/ana/v9r0p2/00/00/11/00/SIM_minerva_00001100_0001_Ana_Tuple_v1_v9r0p2.root")
    TTree *mytree = _file0->Get("CCInclusiveReco")
    mytree->Draw("ev_gate","n_prim_tracks_kinked>0")

    TTree *mytree = _file0->Get("RecoTracks");

Trees - Draw
------------

    mytree->Draw("myvar","","",1)      # 1 event
    mytree->Draw("myvar","","",1,10)   # 1 event, use 10th event
    mytree->Draw("myvar","","",10,10)  # 10 events, start with 10th

Trees - Print
-------------

    mytree->Scan("myvar[0]","","",1,1)  # print element 0 of myvar array (1 event, start at 1)

Math
-----

    root [3] TMath::Factorial(3)
    (Double_t)6.00000000000000000e+00
    root [6] TMath::Factorial(3)*TMath::Factorial(3)/TMath::Factorial(6)
    (double)5.00000000000000028e-02
    root [7] 36/720
    (const int)0
    root [8] double(36/720)
    (const double)0.00000000000000000e+00
    root [9] 36./720.
    (const double)5.00000000000000028e-02
    root [10] double(36)/720
    (const double)5.00000000000000028e-02


Classes
-------

http://www-glast.slac.stanford.edu/software/root/howto/writing_root_classes.htm

