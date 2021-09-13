# Web Management UI documentation
Documentation for the Web management UI ([prod](
https://www.covidcertificate.admin.ch/
) - [test](
https://www.covidcertificate-a.admin.ch/
))

# Table of contents
- [Web Management UI documentation](#web-management-ui-documentation)
- [How to generate multiple COVID certificates ?](#how-to-generate-multiple-covid-certificates--)
  * [General informations](#general-informations)
  * [Certificate types](#certificate-types)
  * [Delivery methods](#delivery-methods)
  * [Templates](#templates)
  * [Create a CSV with Microsoft Excel](#create-a-csv-with-microsoft-excel)
    + [Supported date format](#supported-date-format)
    + [Supported vaccine (vaccination certificate)](#supported-vaccine--vaccination-certificate-)
- [Troubleshooting](#troubleshooting)

# How to generate multiple COVID certificates ?
## General informations

The **Generate multiple certificates** function allows you to create and deliver several certificates by importing a CSV file. The import file can be produced using one of the available [templates](#templates).

⚠️ The CSV file supports until 100 entries and can't exceed a size of 40kB. If you have more data, we recommend to script the process with the [API](
https://github.com/admin-ch/CovidCertificate-Api-Scripts
).

## Certificate types
Three (3) types of certificate can be created:
- vaccination
- test
- recovery

## Delivery methods
Three (3) types of delivery method can be used:
- sent per post
  - **only** available for **vaccination certificates** and **recovery certificates**
  - the certificates will be printed and sent per post
    - the patient [address](
      https://github.com/admin-ch/CovidCertificate-Apidoc#address-data
      ) is required
    - only available for addresses in Switzerland
  - certificates in PDF format will be compressed in a ZIP file and downloaded
- transfer to the mobile app
  - available for all certificate types
  - the certificate is delivered directly in the mobile application (minimum v. 2.2.0) of the patient
  - the patient has to provide an app transfer code
    - *inAppDeliveryCode* can be generated in the mobile application (min. v. 2.2.0)
    - app tranfer code expire 7 days after generation of the code
    - only one certificate is delivered per app transfer code
  - certificates in PDF format will be compressed in a ZIP file and downloaded
- PDF only
  - available for all certificate types
  - certificates in PDF format will be compressed in a ZIP file and downloaded

The specifications regarding the field values of the CSV are the same as for the API. Use the [API documentation](
https://github.com/admin-ch/CovidCertificate-Apidoc#request---certificate-data
) to choose the appropriate values sets for the fields of the CSV.

## Templates
<table>
 <tr>
  <td>&nbsp;</td>
  <td>&nbsp;post</td>
  <td>&nbsp;appTransfer</td>
  <td>&nbsp;PDF only</td>
 </tr>
 <tr>
  <td>&nbsp;vaccination</td>
  <td>&nbsp;<a href="https://github.com/admin-ch/CovidCertificate-UIdoc/blob/main/template-cc_vaccination-delivery_post.xlsx">template-cc_vaccination-delivery_post</a></td>
  <td>&nbsp;<a href="https://github.com/admin-ch/CovidCertificate-UIdoc/blob/main/template-cc_vaccination-delivery_appTransfer.xlsx">template-cc_vaccination-delivery_appTransfer</a></td>
  <td>&nbsp;<a href="https://github.com/admin-ch/CovidCertificate-UIdoc/blob/main/template-cc_vaccination.xlsx">template-cc_vaccination</a></td>
 </tr>
 <tr>
   <td>&nbsp;test</td>
  <td>&nbsp;not available</td>
  <td>&nbsp;<a href="https://github.com/admin-ch/CovidCertificate-UIdoc/blob/main/template-cc_test-delivery_appTransfer.xlsx">template-cc_test-delivery_appTransfer</a></td>
  <td>&nbsp;<a href="https://github.com/admin-ch/CovidCertificate-UIdoc/blob/main/template-cc_test.xlsx">template-cc_test</a></td>
 </tr>
 <tr>
   <td>&nbsp;recovery</td>
  <td>&nbsp;<a href="https://github.com/admin-ch/CovidCertificate-UIdoc/blob/main/template-cc_recovery-delivery_post.xlsx">template-cc_recovery-delivery_post</a></td>
  <td>&nbsp;<a href="https://github.com/admin-ch/CovidCertificate-UIdoc/blob/main/template-cc_recovery-delivery_appTransfer.xlsx">template-cc_recovery-delivery_appTransfer</a></td>
  <td>&nbsp;<a href="https://github.com/admin-ch/CovidCertificate-UIdoc/blob/main/template-cc_recovery.xlsx">template-cc_recovery</a></td>
 </tr>
</table>

## Create a CSV with Microsoft Excel

We recommend Microsoft Excel to edit the template.
1. Open the template with Microsoft Excel.
2. Fill the cells under the titled column with the respectives informations of your patients.
3. Generate the CSV:
 - Windows: ***File*** -> ***Save As*** -> ***Browse*** -> ***Save as type: CSV (Comma delimited)***
 - Mac: ***File*** -> ***Save As...*** -> ***File Format: CSV UTF-8 (Comma-delimited (.csv)***

⚠️ It is possible that when you edit the file with Excel, the date formats are modified. Please note that the date format must follow the specification. You can open the csv file with a text editor in order to check that everything is ok.

### Supported date format for all dates
It is not possible to mix formats, only one of the following formats must be used in a document:
- yyyy-MM-dd (e.g. 2021-06-17)
- dd.MM.yyyy (e.g. 17.06.2021)

### Supported date format for bithdates only
It is not possible to mix formats, only one of the following formats must be used in a document:
- yyyy-MM-dd (e.g. 2021-06-17)
- dd.MM.yyyy (e.g. 17.06.2021)
- yyyy-MM (e.g. 2021-09)
- yyyy (e.g. 2021)

### Supported vaccine (vaccination certificate)
The *medicinalProductCode* has to be one one of the following code:

| description                                                  | medicinalProductCode         |
|--------------------------------------------------------------|--------------|
| Comirnaty vaccine from BioNTech Manufacturing GmbH           | **EU/1/20/1528** |
| COVID-19 Vaccine Moderna from Moderna Biotech Spain, S.L.    | **EU/1/20/1507** |
| COVID-19 Vaccine Janssen from Janssen-Cilag International NV | **EU/1/20/1525** |

### Supported rapid antigen tests
The application supports a dedicated list of rapid antigen tests. Those can be found in [supported rapid antigen tests](https://corona-fachinformationen.bagapps.ch/documents/sars-cov-2-antigen-schnelltests-fachanwendung-mit-covid-zertifikat.pdf).

# Troubleshooting
If the imported CSV file can't be processed because of an error, then an error file will be sent back and no COVID certificates will be produced and delivered.
In this case, fix the errors in the CSV file according to the error description in the returned file.
