# Copyright (C) 1995-2019, Rene Brun and Fons Rademakers.
# All rights reserved.
#
# For the licensing terms see $ROOTSYS/LICENSE.
# For the list of contributors see $ROOTSYS/README/CREDITS.

# Test library loads during importing ROOT
# Testing only the Linux systems is sufficient to detect unwanted links to libraries at import time.
# Mac (and potentially Windows) pull in many system libraries which makes this test very complex.
if (NOT APPLE AND NOT WIN32)
    ROOT_ADD_PYUNITTEST(pyroot_import_load_libs import_load_libs.py)
endif()

# Test ROOT module
ROOT_ADD_PYUNITTEST(pyroot_root_module root_module.py)

# General pythonizations
ROOT_ADD_PYUNITTEST(pyroot_pyz_pretty_printing pretty_printing.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_array_interface array_interface.py DEPENDENCIES_FOUND ${NUMPY_FOUND})

# TObject and subclasses pythonisations
ROOT_ADD_PYUNITTEST(pyroot_pyz_tobject_contains tobject_contains.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tobject_comparisonops tobject_comparisonops.py)

# TClass pythonisations
ROOT_ADD_PYUNITTEST(pyroot_pyz_tclass_dynamiccast tclass_dynamiccast.py)

# TDirectory and subclasses pythonizations
ROOT_ADD_PYUNITTEST(pyroot_pyz_tdirectory_attrsyntax tdirectory_attrsyntax.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tdirectoryfile_attrsyntax_get tdirectoryfile_attrsyntax_get.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tfile_attrsyntax_get_writeobject_open tfile_attrsyntax_get_writeobject_open.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tfile_constructor tfile_constructor.py)

# TTree and subclasses pythonizations
file(COPY TreeHelper.h DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
ROOT_ADD_PYUNITTEST(pyroot_pyz_ttree_branch_attr ttree_branch_attr.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_ttree_iterable ttree_iterable.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_ttree_setbranchaddress ttree_setbranchaddress.py DEPENDENCIES_FOUND ${NUMPY_FOUND})
ROOT_ADD_PYUNITTEST(pyroot_pyz_ttree_branch ttree_branch.py DEPENDENCIES_FOUND ${NUMPY_FOUND})
if (dataframe)
    ROOT_ADD_PYUNITTEST(pyroot_pyz_ttree_asmatrix ttree_asmatrix.py DEPENDENCIES_FOUND ${NUMPY_FOUND})
endif()

# TH1 and subclasses pythonizations
ROOT_ADD_PYUNITTEST(pyroot_pyz_th1_operators th1_operators.py)

# TGraph, TGraph2D and error subclasses pythonizations
ROOT_ADD_PYUNITTEST(pyroot_pyz_tgraph_getters tgraph_getters.py)

# TCollection and subclasses pythonizations
ROOT_ADD_PYUNITTEST(pyroot_pyz_tcollection_len tcollection_len.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tcollection_listmethods tcollection_listmethods.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tcollection_operators tcollection_operators.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tcollection_iterable tcollection_iterable.py)

# TSeqCollection and subclasses pythonizations
ROOT_ADD_PYUNITTEST(pyroot_pyz_tseqcollection_itemaccess tseqcollection_itemaccess.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tseqcollection_listmethods tseqcollection_listmethods.py)

# TIter pythonisations
ROOT_ADD_PYUNITTEST(pyroot_pyz_titer_iterator titer_iterator.py)

# TClonesArray pythonisations
ROOT_ADD_PYUNITTEST(pyroot_pyz_tclonesarray_itemaccess tclonesarray_itemaccess.py)

# TArray and subclasses pythonizations
ROOT_ADD_PYUNITTEST(pyroot_pyz_tarray_len tarray_len.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tarray_getitem tarray_getitem.py)

# TVectorT pythonisations
ROOT_ADD_PYUNITTEST(pyroot_pyz_tvectort_len tvectort_len.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tvectort_getitem tvectort_getitem.py)

# TVector3 pythonisations
ROOT_ADD_PYUNITTEST(pyroot_pyz_tvector3_len tvector3_len.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tvector3_getitem tvector3_getitem.py)

# TString pythonisations
ROOT_ADD_PYUNITTEST(pyroot_pyz_tstring_len tstring_len.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tstring_str_repr tstring_str_repr.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tstring_comparisonops tstring_comparisonops.py)

# TString converter
ROOT_ADD_PYUNITTEST(pyroot_conv_tstring tstring_converter.py)

# TObjString pythonisations
ROOT_ADD_PYUNITTEST(pyroot_pyz_tobjstring_len tobjstring_len.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tobjstring_str_repr tobjstring_str_repr.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_tobjstring_comparisonops tobjstring_comparisonops.py)

# RVec and subclasses pythonizations
ROOT_ADD_PYUNITTEST(pyroot_pyz_rvec rvec.py)
ROOT_ADD_PYUNITTEST(pyroot_pyz_rvec_asrvec rvec_asrvec.py DEPENDENCIES_FOUND ${NUMPY_FOUND})

# RDataFrame and subclasses pythonizations
if (dataframe)
    ROOT_ADD_PYUNITTEST(pyroot_pyz_rdataframe_asnumpy rdataframe_asnumpy.py DEPENDENCIES_FOUND ${NUMPY_FOUND})
    ROOT_ADD_PYUNITTEST(pyroot_pyz_rdataframe_makenumpy rdataframe_makenumpy.py DEPENDENCIES_FOUND ${NUMPY_FOUND})
endif()

# RTensor pythonizations
if (dataframe)
    ROOT_ADD_PYUNITTEST(pyroot_pyz_rtensor rtensor.py DEPENDENCIES_FOUND ${NUMPY_FOUND})
endif()

# Passing Python callables to ROOT.TF
ROOT_ADD_PYUNITTEST(pyroot_pyz_tf_pycallables tf_pycallables.py)

if(roofit)
  # RooAbsCollection and subclasses pythonizations
  ROOT_ADD_PYUNITTEST(pyroot_pyz_rooabscollection_len rooabscollection_len.py)

  # RooDataHist pythonisations
  ROOT_ADD_PYUNITTEST(pyroot_pyz_roodatahist_ploton roodatahist_ploton.py)

  # RooWorkspace pythonizations
  ROOT_ADD_PYUNITTEST(pyroot_pyz_rooworkspace rooworkspace.py)
endif()

# std::string_view backport in CPyCppyy
if (dataframe)
    ROOT_ADD_PYUNITTEST(pyroot_string_view_backport string_view_backport.py)
endif()

# Test wrapping Python callables for use in C++ using numba
if (dataframe)
    ROOT_ADD_PYUNITTEST(pyroot_numbadeclare numbadeclare.py)
endif()

# TComplex pythonizations
ROOT_ADD_PYUNITTEST(pyroot_tcomplex tcomplex_operators.py)
