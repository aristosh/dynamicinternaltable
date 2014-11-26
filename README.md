dynamicinternaltable
====================

Internal Table with dynamic columns in ABAP (defined at run time).
Provides methods for APPEND, READ TABLE, READ TABLE BINARY SEARCH, SORT, and others (see methods list for detail)

###Example
```
DATA ref_it TYPE REF TO zcl_zca_dynamic_table.
DATA ref_wa TYPE REF TO zcl_zca_dynamic_struc.
DATA ref_it_data TYPE REF TO data.
DATA ref_wa_data TYPE REF TO data.
FIELD-SYMBOLS <it> TYPE STANDARD TABLE.
FIELD-SYMBOLS <wa> TYPE ANY.

" define structure
wa-fname = 'f1'.
wa-ftype = 'i'.
APPEND wa TO it.
wa-fname = 'f2'.
wa-ftype = 'char50'.
APPEND wa TO it.
wa-fname = 'f3'.
wa-ftype = 'i'.
APPEND wa TO it.

" create dynamic INTERNAL TABLE object
CREATE OBJECT ref_it
  EXPORTING
    im_it_struc_def = it.

" create dynamic WORK AREA object
CREATE OBJECT ref_wa
  EXPORTING
    im_it_struc_def = it.
    
" assign value to 'work area'
ref_wa->set_value( im_name = 'f1' im_value = 4 ).
ref_wa->set_value( im_name = 'f2' im_value = 'Welcome' ).
ref_wa->set_value( im_name = 'f3' im_value = 69 ).

" append 'work area' to 'internal table'
ref_it->append( ref_wa ).
```
