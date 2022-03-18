# Salesforce -> Developer Beginner -> Formulas and Validations -> Create Validation Rules

## Learning Objectives

- Describe two use cases for validation rules.
- List the elements of a validation rule.
- Create a validation rule.

## Introduction to Validation Rules

Validation rules verify that data entered by users in records meets the standards you specify before they can save it. A validation rule can contain a formula or expression that evaluates the data in one or more fields and returns a value of “True” or “False.” When the validation rule returns a value of "True", this confirms that the data entered by the user contains an invalid value. Validation rules can also include error messages to display to users when they enter invalid values based on specified criteria. Using these rules effectively contributes to quality data. For example, you can ensure that all phone number fields contain a specified format or that discounts applied to certain products never exceed a defined percentage.

## Defining Validation Rules

You can create validation rules for objects, fields, campaign members, or case milestones. In these steps, we create a validation rule that fires when a user tries to save an account with an account number of incorrect length.

## Creating a Validation Rule

1. From Setup, go to Object Manager and click `Account`.
2. In the left sidebar, click `Validation Rules`.
3. Click `New`.
4. Enter the following properties for your validation rule:
     a. Rule Name: Account_Number_8_Characters
     b. Error Condition Formula:

    ![LEN( AccountNumber) != 8](/assets/error-condition-formula.png)

5. Error Message: Account number must be 8 characters long.
6. To check your formula for errors, click `Check Syntax`.
7. Click `Save` to finish.

Here’s how a validation rule’s error message can appear when a user types an incorrect account number format into a field.

![A filled out validation rule, including a related error message that the Account Number must be 8 characters long.](/assets/validation-rule-example-1.png)

## Examples of Validation Rules

Here are some validation rule examples that you can try out yourself.

## Account Number Is Numeric

The AND function returns a value of "True" if all values in the formula are true, and a value of "False" if one or more values are false. The ISBLANK function determines if an expression has a value. The ISNUMBER function determines if an expression's value is a number. The NOT function determines if the inverse of an expression is true. In the example, the validation rule determines if an account number is both not blank and not a number. A value of "True" indicates that the data entered by the user contains an invalid value. That is, if the user enters a non-numeric value for an account number, the validation rule returns a response of "True" and sends an error message .  

| Field | Value |
| ----- | ----- |
| Description: | Validates that the Account Number is numeric if not blank. |
| Formula: |
    1. **AND**(
    2. **NOT**(**ISBLANK**(AccountNumber)),
    3. **NOT**(**ISNUMBER**(AccountNumber))
    4. )`

| Field | Value |
| ----- | ----- |
| Error Message: | Account Number is not numeric. |
| Error Location: | Account Number |

## Date Must Be in the Current Year

The YEAR function returns the four-digit year of a given date. The TODAY function returns the current date. The <> (Not Equal) operator determines if a value is not equal to another value (if it is either less than or greater than the other value.) In the example, the validation rule determines if the year of a given date is not equal to the year of today’s date. A value of "True" indicates that the data entered by the user contains an invalid value. That is, if the user enters a date that is not in the current year, the validation rule returns a response of "True" and sends an error message.

| Field | Value |
| ----- | ----- |
| Description: | Validates that a custom date field contains a date within the current year. |
| Formula: | `YEAR( My_Date__c ) <> YEAR ( TODAY() )` |
| Error Message: | Date must be in the current year. |
| Error Location: | My Date |

## Number Range Validation

In the example, the validation rule determines if the difference between two values (Salary Max and Salary Min) is greater than $20,000. A value of "True" indicates that the data entered by the user contains an invalid value. That is, if the user enters two values whose difference exceeds the $20,000 salary range, the validation rule returns a response of "True" and sends an error message.

| Field | Value |
| ----- | ----- |
| Description: | Validates that the range between two custom fields, Salary Min and Salary Max, is no greater than $20,000. |
| Formula: | `(Salary_Max__c - Salary_Min__c) > 20000` |
| Error Message: | Salary range must be within $20,000. Adjust the Salary Max or Salary Min values. |
| Error Location: | Salary Max |

## Website Extension

The AND function returns a value of "True" if all values in the formula are true, and a value of "False" if one or more values are false. The <> (Not Equal) operator determines if a value is not equal (is either less than or greater than) another value. In the example, if the user enters a website URL with an extension that is not equal to (is either greater than or less than)  all six of the valid extensions, the validation rule returns a response of "True" and sends an error message. If the user enters a website URL with an extension that is identical to (is not greater than or less than) one of the valid extensions, the validation rule returns a response of "False" and does not send an error message, because the data the user entered is valid.

| Field | Value |
| ----- | ----- |
| Description: | Validates a custom field called Web Site to ensure that its last four characters are in an explicit set of valid website extensions. |
| Formula: |
    AND(
      RIGHT( Web_Site__c, 4) <> ".COM",
      RIGHT( Web_Site__c, 4) <> ".com",
      RIGHT( Web_Site__c, 4) <> ".ORG",
      RIGHT( Web_Site__c, 4) <> ".org",
      RIGHT( Web_Site__c, 4) <> ".NET",
      RIGHT( Web_Site__c, 4) <> ".net"
    )
| Field | Value |
| --- | --- |
| Error Message: | Web Site must have an extension of .com, .org, or .net . |
| Error Location: | Web Site |

## Valid Billing Country

The OR function returns a "True" response if one or more expressions in the formula are true, and returns a "False" response if all expressions are false. The LEN function returns the number of characters in a specified text string. In the example, the validation rule determines if the value that the user entered for a Billing Country code is either one character (instead of the required two), or does not contain one of the valid two-character codes. If either of these conditions is true, the validation rule returns a value of "True" and sends an error message. If the user enters a valid Billing Country code, both expressions in the formula are false: the LEN is not 1, and the data does contain one of the valid values. In this case, the validation rule returns a value of "False" and does not send an error message.

| Field | Value |
| ----- | ----- |
| Description: | Validates that the account Billing Country is a valid ISO 3166 two-letter code. |
| Formula: |
    OR(
    LEN(BillingCountry) = 1,
    NOT(
    CONTAINS(
    "AF:AX:AL:DZ:AS:AD:AO:AI:AQ:AG:AR:AM:" &
    "AW:AU:AZ:BS:BH:BD:BB:BY:BE:BZ:BJ:BM:BT:BO:" &
    "BA:BW:BV:BR:IO:BN:BG:BF:BI:KH:CM:CA:CV:KY:" &
    "CF:TD:CL:CN:CX:CC:CO:KM:CG:CD:CK:CR:CI:HR:" &
    "CU:CY:CZ:DK:DJ:DM:DO:EC:EG:SV:GQ:ER:EE:ET:FK:" &
    "FO:FJ:FI:FR:GF:PF:TF:GA:GM:GE:DE:GH:GI:GR:GL:" &
    "GD:GP:GU:GT:GG:GN:GW:GY:HT:HM:VA:HN:HK:HU:" &
    "IS:IN:ID:IR:IQ:IE:IM:IL:IT:JM:JP:JE:JO:KZ:KE:KI:" &
    "KP:KR:KW:KG:LA:LV:LB:LS:LR:LY:LI:LT:LU:MO:MK:" &
    "MG:MW:MY:MV:ML:MT:MH:MQ:MR:MU:YT:MX:FM:MD:MC:" &
    "MC:MN:ME:MS:MA:MZ:MM:MA:NR:NP:NL:AN:NC:NZ:NI:" &
    "NE:NG:NU:NF:MP:NO:OM:PK:PW:PS:PA:PG:PY:PE:PH:" &
    "PN:PL:PT:PR:QA:RE:RO:RU:RW:SH:KN:LC:PM:VC:WS:" &
    "SM:ST:SA:SN:RS:SC:SL:SG:SK:SI:SB:SO:ZA:GS:ES:" &
    "LK:SD:SR:SJ:SZ:SE:CH:SY:TW:TJ:TZ:TH:TL:TG:TK:" &
    "TO:TT:TN:TR:TM:TC:TV:UG:UA:AE:GB:US:UM:UY:UZ:" &
    "VU:VE:VN:VG:VI:WF:EH:YE:ZM:ZW",
    BillingCountry)))
| Field | Value |
| ----- | ----- |
| Error Message: | A valid two-letter country code is required. |
| Error Location: | Billing Country |

## Resources

- [Salesforce Help: Validation Rules](https://help.salesforce.com/articleView?id=fields_about_field_validation.htm&type=5)
- [Salesforce Help: Managing Validation Rules](https://help.salesforce.com/articleView?id=fields_managing_field_validation.htm&type=5)
- [Salesforce Help: Tips for Writing Validation Rules](https://help.salesforce.com/articleView?id=fields_validation_rules_tips.htm&type=5)
