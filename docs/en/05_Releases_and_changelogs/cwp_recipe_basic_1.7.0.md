# CWP Recipe 1.7.0

## Overview

This upgrade includes CMS and Framework version 3.6.1 which includes bugfixes and 
some minor feature and API enhancements.

 * [framework 3.6.1](https://github.com/silverstripe/silverstripe-framework/blob/3.6/docs/en/04_Changelogs/3.6.1.md)

Upgrade to Recipe 1.7.0 is optional, but is recommended for all CWP sites. 

This upgrade can be carried out by any development team familiar with SilverStripe CMS, but if you
would like SilverStripe's assistance, please let us know.

## Upgrading Instructions

In order to update an existing site to use the new basic recipe the following changes to your composer.json
can be made:

```json
"require": {
    "cwp/cwp-recipe-basic": "~1.7.0@stable",
    "cwp/cwp-recipe-blog": "~1.7.0@stable",
    "cwp/starter-theme": "~1.1.0@stable"
},
"prefer-stable": true
```

## Accepted failing tests

In recipe 1.7.0 these module unit tests cause external errors, but do not represent legitimate issues.

#### silverstripe/framework

 * UploadFieldTest.testAllowedExtensions — Behaviour intentionally altered by the MimeValidator module
 * UploadFieldTest.testSelect — Behaviour altered by SelectUploadField intentionally
 * UploadTest.testUploadTarGzFileTwiceAppendsNumber — This test is now expected
   to fail as the new MimeValidator module will no longer allow random content to
   be uploaded with a mismatched mime and file extension. The original test is
   attempting to upload a bunch of text as a gzip file.

#### silverstripe/queuedjobs

 * QueuedJobsTest.testImmediateQueuedJob - Test self-aborts when detecting lack of available system
   resources (inconclusive).
 * QueuedJobsTest.testStartJob - Test self-aborts when detecting lack of available system
   resources (inconclusive).

#### silverstripe/translatable

 * TranslatableSearchFormTest.testPublishedPagesMatchedByTitleInDefaultLanguage - Test failure
   affected by global state. See https://github.com/silverstripe/silverstripe-translatable/issues/223
 * TranslatableSiteConfigTest.testCanEditTranslatedRootPages - Test failure affected by global state.
   See https://github.com/silverstripe/silverstripe-translatable/issues/224

#### silverstripe/userforms

 * UserDefinedFormControllerTest.testValidation - Test failure affected by global state (starter theme template overrides).
 * UserDefinedFormControllerTest.testRenderingIntoFormTemplate - Test failure affected by global state.
 * UserDefinedFormControllerTest.testRenderingIntoTemplateWithSubstringReplacement - Test failure affected by global state.

## Change Log

### Security

 * 2017-05-25 [25b77a2ff](https://github.com/silverstripe/silverstripe-framework/commit/25b77a2ff8deabe8e8894002b9a5647eaec27b0a) SVG uploads disabled by default (Daniel Hensby) - See [ss-2017-017](http://www.silverstripe.org/download/security-releases/ss-2017-017)

### Features and Enhancements

 * 2017-09-08 [3e847a4](https://gitlab.cwp.govt.nz/cwp/starter-theme/commit/3e847a4a02c49fedd3d5cab21656fccd4a5edc9d) Only show header search form if one exists to use (Robbie Averill)
 * 2017-07-16 [a626d0a](https://github.com/silverstripe/silverstripe-userforms/commit/a626d0a66e23b7c7173ba1b42388c92b8c061eb7) Update GridField creation to be injectable (Franco Springveldt)
 * 2017-07-12 [0f841cd](https://github.com/silverstripe/silverstripe-userforms/commit/0f841cd982d0bd5a5ad349ec5c116a8acb4f0581) Use a paragraph instead of a label for literal field titles (Robbie Averill)
 * 2017-07-11 [1b472cd](https://github.com/silverstripe/silverstripe-userforms/commit/1b472cda7b175a73ba44be1b9121a21a3ec0de0d) removed needless list from CheckboxGroupField and RadioField (Franco Springveldt)
 * 2017-06-29 [eb89925](https://gitlab.cwp.govt.nz/cwp/cwp-recipe-basic/commit/eb89925de1e3cca0c90936c75d17a410e01612ec) update PHP version constraint to &gt;=5.6 (Franco Springveldt)
 * 2017-06-17 [5ad7767](https://github.com/silverstripe/silverstripe-userforms/commit/5ad7767ead3933d01a9bb839559681efae03f386) Display and export the submitter email (Cam Findlay)
 * 2017-05-15 [8107cff](https://github.com/silverstripe/silverstripe-taxonomy/commit/8107cff5a6ba4ae0c53c3e296a740fd329d3604f) Add TaxonomyType to group taxonomy terms by different types (Robbie Averill)

### Bugfixes

 * 2017-09-26 [8e684de](https://github.com/silverstripe/silverstripe-blog/commit/8e684dea507a5bf54c812c40d900b31dc44aa856) BlogArchiveWidget for PostgreSQL compatibility (Robbie Averill)
 * 2017-09-22 [27044d8](https://github.com/silverstripe/silverstripe-blog/commit/27044d86a52b8113a0f447e658feafad3d7b6435) Display individual years in blog archive widget when set to "Yearly" (Robbie Averill)
 * 2017-09-21 [df04582](https://github.com/silverstripe/silverstripe-lumberjack/commit/df04582530a7e57ea446740cdf5c96a085ce5eaf) visibility for excludeSiteTreeClassNames changed and doc update (Franco Springveldt)
 * 2017-09-19 [dd99980](https://github.com/silverstripe/silverstripe-lumberjack/commit/dd99980370ab64f736847d83b470a5a0cd703648) only exclude SiteTree subclasses if they are set (Franco Springveldt)
 * 2017-09-01 [2631175](https://github.com/silverstripe/silverstripe-blog/commit/26311750b984488c02480cb27b18b566c562e004) Encode URLSegment to support multibyte member profile URLs (Robbie Averill)
 * 2017-08-28 [277db10](https://gitlab.cwp.govt.nz/cwp/cwp-recipe-basic/commit/277db10bc7c949f214eab276ecdd492d36ccd55d) gridfieldextensions updated to ^2.0 (Franco Springveldt)
 * 2017-08-28 [e65d91a](https://gitlab.cwp.govt.nz/cwp/cwp-recipe-basic/commit/e65d91a172ce97db0620a8288d2288ee9e3bcfd9) updated versionedfiles version constraint (Franco Springveldt)
 * 2017-08-28 [11e8cc5](https://gitlab.cwp.govt.nz/cwp/cwp-recipe-basic/commit/11e8cc56f14d575b6c7326c0364338de0290b930) updated queuedjobs version constraint (Franco Springveldt)
 * 2017-08-28 [357366d](https://gitlab.cwp.govt.nz/cwp/cwp-recipe-basic/commit/357366d69fcf59559e56da0204878946e9761fbd) updated multivaluefield version constraint (Franco Springveldt)
 * 2017-08-28 [722f9d3](https://github.com/silverstripe/silverstripe-userforms/commit/722f9d3f82b2968dbdec4e76a623bd36ccd6f90b) updated gridfieldextensions constraint (Franco Springveldt)
 * 2017-08-28 [03ae4cc](https://gitlab.cwp.govt.nz/cwp/cwp-recipe-basic/commit/03ae4cc33345abe3a56f1412eb47c8046b5cc779) gridfieldextensions updated to 2.0.x-dev (Franco Springveldt)
 * 2017-08-28 [0ded303](https://gitlab.cwp.govt.nz/cwp/cwp-recipe-basic/commit/0ded3038b929f7726c5e495a4a0702c35085e545) versionedfiles vendor updated to symbiote (Franco Springveldt)
 * 2017-08-28 [34c3ffa](https://gitlab.cwp.govt.nz/cwp/cwp-recipe-basic/commit/34c3ffad622836ac72a8429b6d5da51eb551dede) bumped advancedworkflow version constraint as 4.0.x-dev (Franco Springveldt)
 * 2017-08-28 [da1b715](https://gitlab.cwp.govt.nz/cwp/cwp-recipe-basic/commit/da1b715de77e57ec0b26b8e8a2dc45aa12cd9e46) bumped advancedworkflow version constraint (Franco Springveldt)
 * 2017-08-27 [19bb05b](https://gitlab.cwp.govt.nz/cwp/cwp-recipe-basic/commit/19bb05b4ad9bee73998884ade09d7f4da01498d7) referenced symbiote as a vendor (Franco Springveldt)
 * 2017-08-25 [e2d01ba](https://gitlab.cwp.govt.nz/cwp/cwp-recipe-basic/commit/e2d01badd2e89c2c3f185e7c8b6c4857fa3bb148) loosened core version constraints (Franco Springveldt)
 * 2017-08-24 [1bbef96](https://gitlab.cwp.govt.nz/cwp/cwp-recipe-blog/commit/1bbef9642d5595117c4a634253f45492818a85fd) lumberjack version updated (Franco Springveldt)
 * 2017-08-24 [0d56304](https://gitlab.cwp.govt.nz/cwp/cwp-recipe-basic/commit/0d56304c885ed9885c91c6bc64002eea8eb2ede5) - prepended silverstripe to symbiote module names (Franco Springveldt)
 * 2017-08-22 [19897e0](https://github.com/silverstripe/silverstripe-contentreview/commit/19897e0b8fcf6f4f590366774e35d237efb268ad) Fixes #59 Minor changes wr/t typos. (Russell Michell)
 * 2017-08-21 [afa4e75](https://github.com/silverstripe/silverstripe-userforms/commit/afa4e75f031ab2697d38f06b1cba48f3a6c99e0e) HTML or plain text toggle works across PJAX requests (Robbie Averill)
 * 2017-08-16 [fac99f7](https://github.com/silverstripe/silverstripe-userforms/commit/fac99f7b6b8ea1675737381ca56d850c1f9b075d) Alias object context in closure for PHP 5.3 compat, add test to cover it (Robbie Averill)
 * 2017-08-08 [236bf6d](https://github.com/silverstripe/silverstripe-blog/commit/236bf6d8fc86466a953019319202440f071c8133) added date formatting (Franco Springveldt)
 * 2017-08-03 [06269e8](https://github.com/silverstripe/silverstripe-fulltextsearch/commit/06269e8203169dd680bc9b0350c5283aa02d88a8) Return a non-zero exit code when Solr_Configure has an exception (Robbie Averill)
 * 2017-08-02 [1697cf4](https://gitlab.cwp.govt.nz/cwp/starter-theme/commit/1697cf44131efdfd92016d84745b8bb45bb0148c) Remove title from userforms checkbox holder (Sacha Judd)
 * 2017-07-26 [3a18b9f](https://github.com/silverstripe/silverstripe-blog/commit/3a18b9f69bf8bb406360bcbf1b2ab416455f1397) If BlogPost has date field, return it in getDate (Daniel Hensby)
 * 2017-07-19 [c29438f](https://github.com/silverstripe/silverstripe-blog/commit/c29438fd1a8df1c7890571065940100851ed465f) Dont generate urlsegments if we dont need to (Daniel Hensby)
 * 2017-07-13 [c98fa0b](https://github.com/silverstripe/silverstripe-userforms/commit/c98fa0bab4881d5f1fb62722f1c5e65398232f21) fieldset without a legend shouldn't be a fieldset (Franco Springveldt)
 * 2017-07-09 [8f2aaf5](https://gitlab.cwp.govt.nz/cwp/cwp/commit/8f2aaf5bc276628a60285157fdcd7c035b41f095) ed link formats in performance guide docs (Ingo Schommer)
 * 2017-07-07 [3e7f021](https://github.com/silverstripe/silverstripe-spamprotection/commit/3e7f021de79d65a347cd14a037242bfad7e5bf5d) Compatibility with userforms 3/4 getCMSFields, remove deprecated getSettings use etc (Robbie Averill)
 * 2017-07-06 [a8860d9](https://gitlab.cwp.govt.nz/cwp/cwp/commit/a8860d90495e51de90b65f7ff0334803156dc3ae) formatting errors (Glen Peek)
 * 2017-07-06 [3572328](https://gitlab.cwp.govt.nz/cwp/cwp/commit/357232873526970d85c0ef7c5c327ada32cbdce0) getBaseStyles examples (Glen Peek)
 * 2017-06-30 [c1afb3a](https://github.com/silverstripe/silverstripe-userforms/commit/c1afb3a5bfb345e0f68de0abf44fe4388a32fb9f) Remove css fields animation on add :wrench: (Sacha Judd)
 * 2017-06-26 [1e1b596](https://github.com/silverstripe/silverstripe-userforms/commit/1e1b59673977667e1cfb2e0f093860be0db1eb48) use the correct method for CSV exports and include the full file path (Franco Springveldt)
 * 2017-06-22 [dbe2315](https://gitlab.cwp.govt.nz/cwp/starter-theme/commit/dbe2315e33c38fdd1825f202aa0e61f79660c021) Remove duplicate title attribute content (Robbie Averill)
 * 2017-06-22 [b5da9f9](https://gitlab.cwp.govt.nz/cwp/starter-theme/commit/b5da9f965c08cafae231853c3bb0d99d942f182e) add btn btn-link class for firefox focus (Sacha Judd)
 * 2017-06-21 [899aa2c](https://gitlab.cwp.govt.nz/cwp/starter-theme/commit/899aa2ce452ce54f6c20c9901f6ec4f8ded11f47) add class btn to navbar-touch-caret for focus visible in firefox (Sacha Judd)
 * 2017-06-21 [683ee14](https://github.com/silverstripe/silverstripe-userforms/commit/683ee14428b70358b327dbbd1002463c31008232) Preview recipient email link for SS 3.6 (Robbie Averill)
 * 2017-06-20 [d88ce28](https://github.com/silverstripe/silverstripe-userforms/commit/d88ce281742833205401e1df366a834a8178c61d) Pass submissions GridFieldConfig to GridField constructor to avoid error in state (Robbie Averill)
 * 2017-06-17 [0d6b44a](https://github.com/silverstripe/silverstripe-blog/commit/0d6b44aa44377cbabbc7a538acb29a74092088b8) mysql &gt;= 5.7 sql_mode=only_full_group_by error (Franco Springveldt)
 * 2017-06-15 [9378147](https://gitlab.cwp.govt.nz/cwp/starter-theme/commit/9378147b094153e17049f7c23432d4058c161fd2) add outline-focus status for buttons (Sacha Judd)
 * 2017-06-15 [12198e2](https://github.com/silverstripe/silverstripe-contentreview/commit/12198e21e675ab8e17eddd074a980bda9f341dd1) Remove specific page edit URL from tests to ensure multi SS version compatibility (Robbie Averill)
 * 2017-06-14 [b33a16a](https://gitlab.cwp.govt.nz/cwp/cwp/commit/b33a16a6520e577faaa09630925ffc12b3aa93f4) ADFS docs to account for DR instances (John)
 * 2017-06-14 [7774cff](https://github.com/silverstripe/comment-notifications/commit/7774cffe372910e20679fc4f9943ed2e174b5f41) Bump comments constraint to ^2.0 (Robbie Averill)
 * 2017-06-14 [1073eca2f](https://github.com/silverstripe/silverstripe-framework/commit/1073eca2fac1b05c0e20b02aea78e8a2f550cfe5) Complex (curly) syntax (Marcz Hermo)
 * 2017-06-14 [fd57bd910](https://github.com/silverstripe/silverstripe-framework/commit/fd57bd9100634682fc5b2d9f493e3c54ce0444ad) Update help link from 3.5 to 3.6 (Robbie Averill)
 * 2017-06-12 [c02d851](https://github.com/silverstripe/silverstripe-comments/commit/c02d8515002f7702f2c6ea5227bd8a1e1633fa91) Remove providePermissions tests (Robbie Averill)
 * 2017-06-12 [f0c00bfb7](https://github.com/silverstripe/silverstripe-framework/commit/f0c00bfb7819c0350fa882f899d0c820a2aefa81) ing language typo in docs (3Dgoo)
 * 2017-06-08 [e965942](https://github.com/silverstripe/silverstripe-userforms/commit/e96594247b9b86fd13ae661285312089a034997a) Selector for HTML/plain email content toggle. Show preview button for both. (Robbie Averill)
 * 2017-06-08 [bf20e19](https://github.com/silverstripe/silverstripe-userforms/commit/bf20e19285d2375ce948cab7e6a86a7532f8008a) Ensure HTML email preview content is parsed as HTML including shortcodes (Robbie Averill)
 * 2017-06-08 [c02181e](https://github.com/silverstripe/silverstripe-userforms/commit/c02181e69b4b7b060ac17959d52bf45255769f5e) Use configuration nesting wrapper around themed preview logic (Robbie Averill)
 * 2017-06-08 [6e69972](https://github.com/silverstripe/silverstripe-userforms/commit/6e69972c35047f1c2ff23b126d3951f161aefb84) default values for EditableMultipleOptionField subclasses (Florian Thoma)
 * 2017-06-05 [182cab0](https://gitlab.cwp.govt.nz/cwp/starter-theme/commit/182cab0d7b06511ddcda53ba61325b1e9e30565d) Override Bootstrap .hide definition for userforms formfields (Robbie Averill)
 * 2017-06-05 [15f5b83](https://gitlab.cwp.govt.nz/cwp/starter-theme/commit/15f5b834e5ad3d5aa15130dbd9be526731d3d147) Update userforms holder ID to match default templates (Robbie Averill)
 * 2017-06-05 [51890f6](https://github.com/silverstripe/silverstripe-userforms/commit/51890f6084f88c19b6d6f21b5156e971f8e9ecd5) Remove "hide" class from form inputs, leave it on the field holder - fixes display rules issue (Robbie Averill)
 * 2017-06-02 [a52ed03b4](https://github.com/silverstripe/silverstripe-framework/commit/a52ed03b49b8f62573eb3e295bfde84d1ef68f46) Upgrade old style constructors that were missed (Daniel Hensby)
 * 2017-06-01 [c08bd67](https://gitlab.cwp.govt.nz/cwp/starter-theme/commit/c08bd6770a62eedb4c0183a0a94bd44538ef703b) Escape search term in page title (Robbie Averill)
 * 2017-05-29 [b4368196d](https://github.com/silverstripe/silverstripe-framework/commit/b4368196d1bcee9fd1714b044c8ae6580c7941c9) Use plural name for ModelAdmin tab name (Robbie Averill)
 * 2017-05-24 [ec2b012](https://github.com/silverstripe/silverstripe-userforms/commit/ec2b012eedc92c45493259350f7c248502250f76) incorrect calculation of MAX_FILE_SIZE (#600) (Reece Alexander)
 * 2017-05-02 [0d97864](https://github.com/silverstripe/silverstripe-secureassets/commit/0d97864aa4beac49f0d186db309f8ee6fa2469a3) Viewer Groups not loading, unable to select fixes #55 (Shea)
 * 2017-04-12 [2cd7db9](https://github.com/silverstripe/silverstripe-blog/commit/2cd7db9beb44804f71fd18519d6b39a0e033a3db) Add translation to some areas of BlogMemberExtension that were missing them (Rastislav Brandobur)
 * 2017-04-10 [6b76bc6](https://github.com/silverstripe/silverstripe-userforms/commit/6b76bc641a8855372291b541e2e2fffdf2aaef5c) Ensure field GridField has a 100% relative width rather than fixed (Robbie Averill)
 * 2017-03-16 [dd3efa1](https://github.com/silverstripe/silverstripe-selectupload/commit/dd3efa1c4f2a9f428af8e3e0939ebd31f18cfc30) typo in template variable (Michal Kleiner)
 * 2017-01-31 [262cbf7](https://github.com/silverstripe/silverstripe-userforms/commit/262cbf74c1db72d16e9a6f03ce21d2f776e22c49) jquery validate attempting to validate ul as input (Igor Nadj)
 * 2016-12-19 [99e7e34](https://gitlab.cwp.govt.nz/cwp/cwp/commit/99e7e344c69ccc04dc058f98c5ae161a12fa1921) ed a bug in the generatePDF function where the wkhtmltopdf_binary config option was being ignored. (Mitchell Bennett)