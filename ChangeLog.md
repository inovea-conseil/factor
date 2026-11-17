# Change Log
All notable changes to this project will be documented in this file.

## Unreleased
- Inovea Conseil - Add TIF export and compatibility with listexportimportv2 - *18/04/2026* - 1.6.2 avgp

## Release 1.6
- FIX : COMPAT V24 - *30/06/2026* - 1.6.2
- FIX : DA028299 - Invoice list selection checkboxes were hidden unless a generated PDF already existed - *09/06/2026* - 1.6.1
  + "Select all/none" links not working (jQuery .attr -> .prop)
  + Natixis export used deprecated Societe::code_compta (no longer populated by fetch) -> use code_compta_client, fixes false "missing accounting code" error and blank code in export file
  + PDF merge: generate the invoice PDF on the fly when it is missing, instead of failing with "no PDF available"
  + PDF merge: catch TCPDF/FPDI errors on corrupted/unreadable PDF (skip the file + warning) instead of a raw error on a blank page
  + Guard define('INC_FROM_DOLIBARR') (hook beforePDFCreation + module init) to avoid "constant already defined" warning on multiple PDF generations
- NEW : COMPAT V23 - *01/04/2026* - 1.6

## Release 1.5
- FIX : DA027722 - Fatal false function name - *10/02/2026* - 1.5.3
- FIX : COMPAT V23 - *12/12/2025* - 1.5.2 
- FIX : COMPAT V22 - *18/08/2025* - 1.5.1
- NEW : COMPAT V21 - *20/12/2024* - 1.5.0

## Release 1.4
- NEW : COMPAT V20 - *25/07/2024* - 1.4.0

## Release 1.3
- NEW : TechATM - *10/01/2024* - 1.3.0
- NEW : compat V19 et php8.2 - *11/12/2023* - 1.2.0  
  Changed Dolibarr compatibility range to 15 min - 19 max  
  Change PHP compatibility range to 7.0 min - 8.2 max

## Release 1.1
- FIX : Repetition of the INVOICE_FREE_TEXT constant during a multiple regeneration of documents


## Release 1.0
- FIX : Compatibility V17 PHP8.1 warnings - *21/04/2023* - 1.0.9
- FIX : Compatibility V16 TOKEN - *13/06/2022* - 1.0.8  
  - change family
- FIX : Missing Icon  *25/07/2021* - 1.0.7
- FIX : Compatibility V15 : variables inutilisées supprimées car provoques des warning - 1.0.6
- FIX : v14 compatibility: `f.tva` (now `total_tva`) and `f.total` (now `total_ht`)
  \+ module descriptor - *13/10/2021* - 1.0.5
- FIX : V13 Compatibility Box Module and GETPOST *06/05/2021* - 1.0.4
