# State Inpatient Discharges and Insurance — Methodology and Findings

This document describes the steps BuzzFeed News took to calculate the rates at which freestanding inpatient psychiatric hospitals in Florida and California discharge patients who have commercial insurance versus those classified as self-paying. The analysis provides support for the following two paragraphs from the BuzzFeed News article, “[Intake](https://www.buzzfeed.com/rosalindadams/intake),” published December 7, 2016:

> At the company’s Florida hospitals, between 2013 and 2015, 55% of self-paying patients were discharged within three days, compared with just 30% of patients with commercial insurance. (Other for-profit psychiatric hospitals had a similar disparity, but not-for-profits showed almost no difference.) In California, a similar pattern was found.

> Asked about this discrepancy, Johnson, the vice president of clinical services, said that a patient’s length of stay is based on their individual treatment plan. She disputed that a patient’s insurance was a factor and added that a discharge is “a clinical decision; it’s not a business decision.”

## Table of Contents

- [Data Sources](#data-sources)
- [Data Processing](#data-processing)
- [Findings](#findings)

## Data Sources

The analysis depends on inpatient discharge databases from Florida and California. Due to the sensitivity of these files, the states prohibit users from republishing the raw data or any patient-identifying information.

From Florida, BuzzFeed News obtained [data for all inpatient discharges](http://www.floridahealthfinder.gov/Researchers/OrderData/order-data.aspx) in 2013–2015, the most recent three years available. The latest version of Florida’s data dictionary can be found [here](https://floridahealthfinderstore.blob.core.windows.net/documents/researchers/OrderData/documents/Inpatient%20Data%20Layout%202015Q4%20March%202016.pdf).

From California, BuzzFeed News obtained [analogous data](https://www.oshpd.ca.gov/HID/Products/PatDischargeData/PublicDataSet/) from 2012–2014, the most recent three years available. California’s data dictionary can be found [here](https://www.oshpd.ca.gov/HID/Data_Request_Center/documents/puf/DataDictionary_Public_PDD.pdf).

## Data Processing

### Identifying claims from freestanding inpatient psychiatric hospitals

In the Florida data, discharges from freestanding inpatient psychiatric hospitals were identified as those with a “Mod Code” value of “CL03 – Class 3 Hospital Psychiatric,” defined as “specialty psychiatric hospital offering a restricted range of services appropriate to the diagnosis, care, and treatment of patients with specific categories of psychiatric illnesses or disorders.” BuzzFeed News additionally restricted the Florida data to discharges from hospitals certified to receive involuntarily committed patients under the state’s “Baker Act.” (These hospitals account for 98% of the aforementioned discharges.)

In the California data, analogous discharges were identified as those coming from hospitals listed by the state as having a “license type” of “Acute Psychiatric.”

### Hospital types

BuzzFeed News grouped all discharges into four categories, based on the hospital’s ownership:

- UHS hospitals
- All other for-profit hospitals
- Non-profit hospitals
- Government-run hospitals

### Classifying Insurance Types — Florida

Florida’s discharge data includes a field indicating the expected primary payer at the time of discharge. BuzzFeed News condensed those possible values into six categories: commercial insurance, “self-pay”, Medicare, other public insurance, non-payment (includes charity care, no-charge care, etc.), and “other.” Below are the list of codes BuzzFeed News placed in each category, along with the state’s definition:

#### “Commercial”

- E – Commercial Health Insurance – Patients covered by any type of private coverage, including HMO, PPO, or self-insured plans. (NOTE: Prior to first quarter 2010, Commercial Insurance was reported as Payer “E”. Commercial HMO was reported as Payer ”F” and Commercial PPO was reported as Payer “G”.)

#### “Self-pay”

- L – Self Pay – Patients with no insurance coverage (NOTE: Payer L was defined as Self Pay/ Under-insured prior to first quarter 2010.)

#### “Medicare”

- A – Medicare
- B – Medicare Managed Care – Patients covered by Medicare Advantage plans, Medicare HMO, Medicare PPO, Medicare Private Fee for Service or any other type of Medicare plan where CMS is not the direct payer. (NOTE: Payer B was defined as “Medicare HMO and Medicare PPO”, beginning first quarter 2006 through fourth quarter 2009.) (NOTE: Prior to first quarter 2006, Payer B was defined as Medicare HMO.)

#### “Other Public”

- C – Medicaid
- D – Medicaid Managed Care – Patients covered by Medicaid funded capitated plans. This would include any program where the patient is enrolled in the Medicaid program but the payment is not directly from the state of Florida Medicaid program. (NOTE: Payer D was defined as “Medicaid HMO” prior to first quarter 2010.)
- H – Workers’ Compensation
- I – TriCare or Other Federal Government (NOTE: Payer I was defined as “CHAMPUS” prior to first quarter
    2010.)
- J – VA
- K – Other State/Local Government
- O – Kidcare – Includes Healthy Kids, Medikids, and Children’s Medical Services

#### “Non-payment”

- N – Non-Payment – Includes charity, professional courtesy, no charge, research/clinical trial, refusal to pay/bad debt, Hill Burton free care, research/donor that is known at the time of reporting. (NOTE: Payer N was defined as “Charity” prior to first quarter 2010.)

#### “Other”

- M – Other
- Q – Commercial Liability Coverage – Patients whose health care is covered under a liability policy, such as automobile, homeowners or general business. (NOTE: Payer Q is a new code effective first quarter 2010.)

### Classifying Insurance Types — California

California uses a similar classification system for the expected primary payer. BuzzFeed News’s categorizations, along with the state’s definition:

#### “Commercial”

- 03 = Private Coverage

#### “Self-Pay”

- 08 = Self Pay

#### “Medicare”

- 01 = Medicare

#### “Other Public”

- 02 = Medi-Cal
- 04 = Workers’ Compensation
- 05 = County Indigent Programs
- 06 = Other Government
- 07 = Other Indigent

#### “Other”

- 09 = Other Payer
- 00 = Invalid/Blank

### Lengths of stay

Both databases contain a field directly indicating the discharged patient’s length of stay, measured in days.

### Other variables

Both databases include a field indicating the patient’s “Medicare Severity-Diagnosis Related Group” (MS-DRG) classification. MS-DRG 885 corresponds to “psychoses.”

The Florida database includes the patient’s age and race/ethnicity; the California database does not.

## Findings

The findings, and the code used to produce them, can be [found here](notebooks/inpatient-discharge-analysis.ipynb).

## Questions / Comments?

Please contact Jeremy Singer-Vine at jeremy.singer-vine@buzzfeed.com.

Looking for more from BuzzFeed News? [Click here for a list of our open-sourced projects, data, and code](https://github.com/BuzzFeedNews/everything).
