**Input validation** is a technique that is used to limit the user input for attaining just the required functionality through input testing. Since some of the vulnerabilities like XSS, SQL Injection, SSTI, etc. are possible due to lack of implementation within input validation, it is necessary to understand what we are able to implement to prevent these vulnerabilities and prevent any of the **Confidentiality**, **Integrity**, and **Availability** issues. Since different programming languages offer different methods to validate the input, the mechanism of either **whitelisting** or **blacklisting** remains the same for all languages.

The validation must be done within both the **Syntactical** and **Semantic** Levels.

## Syntactical Level
From the name, we are able to guess that the syntactical is related to the syntax of any input. Hence, the syntax of the structured fields needs to be validated.

**For example:**
_**Phone Number**:_ +9779812345678, which shows that we have a + symbol at the beginning of the syntax followed by a country code that could be between 1 to 3 in length along with the phone number, 10 in length allowing only digits from 0 to 9.

## Semantic Level
Semantics comes to play when the correctness of the values is within the required context. 

**For example:**
**Dates**: Allowing dates with limits where required. If a date for a user’s enrolment within a university is given, the semantic validation should not allow the user to enter any dates before the enrolment date for graduation.

# Implementation of input validation 
Some of the new developers working without frameworks usually only handle the validation on the frontend part making the application vulnerable when the requests are modified through different tools like Burp Suite or even the browser’s ability to modify and resend requests.

Hence, validation should be done for both the front end and the back end. But most of the input validation is already available in frameworks such as Django which gives the developers ease in implementing these validations. But some of the validation needs to be done according to the cases we see.

**The following are the ways to set validations:**

- Checks for specific schemas such as JSON, XML, etc., and including strict checks for validation.
- Using exception handling to handle special cases and using data types to specify the type of data being input rather than using strings for every data type.
- The range of the characters should be checked and limited so that no more than the specified range can be input.
- Using regular expressions must be done to cover the whole string rather than just sections of the string i.e. using the ^ to scan from the starting of the string and $ till the end to make sure the whole string is selected rather than a substring involved.
- Only allow a set of required characters to be accepted
- Using encoding to encode special characters that need to be output to the page or application
- Validate the same set of rules for the name of the uploads for the files and rename them randomly using UUIDs or any naming convention that is very random.
- Validate the size of the uploaded file and the extension of the file. The extension of the file must be validated and limited.
- For files that are zipped and uncompressed later by the server, validation of the zip needs to be done beforehand which includes the target path, level of compression, and the estimated size of the decompressed file.
- The uploaded files need to be scanned for any malicious content and need to be verified.
- The file path of the file must be set from the server side (backend) not the client side (frontend)
- The content type of the uploaded file must be predefined and served accordingly. Executable scripts, configuration files, and other cross-domain config files must be blocked from uploading.
- Using image rewriting libraries to verify the validity of the image and removal of excess content should be done. The image must be set to be of certain formats only. Some feel that stopping the extension of the file would be a good solution but the content of the image needs to be checked beforehand as there are executable scripts that can be renamed and uploaded.
- Strict email address validation needs to be done from the client side as well as the server side. [https://tools.ietf.org/html/rfc5321#section-4.1.2](https://tools.ietf.org/html/rfc5321#section-4.1.2) defines the format of the email addresses. Using regex to have syntactic validation and using techniques to verify through semantic validation that the email actually exists is a way to validate emails.
- Blacklisting email addresses that are disposable could be a solution but since domains can be created and creating a mail server is very easy, the process to blacklist could be endless. So, whitelisting of email addresses could be done wherever possible.

Hence by following the above methods to whitelist and blacklist a set of syntactic rules and following some semantic procedures, we are able to validate data that has been input.

# What to Do When Input Fails Validation?

So, what do you do when input fails validation? There are two major approaches: **recovering** and continuing on, or **failing** the action and reporting an error. Each has its advantages and disadvantages:
## Recovering
Recovering from an input validation failure implies that the input can be sanitized or fixed — that is, that the problem that caused the failure can be solved programmatically. This is generally more likely to be possible if you are taking a blacklisting approach for input validation, and it commonly takes the approach of removing bad characters from the input. The major disadvantage of this approach is ensuring that the filtering or removal of values does actually sanitize the input, and doesn’t just mask the [malicious input](https://www.sciencedirect.com/topics/computer-science/malicious-input), which can still lead to SQL injection issues.
## Failing
Failing the action entails generating a security error, and possibly redirecting to a generic error page indicating to the user that the application had a problem and cannot continue. This is generally the safer option, but you should still be careful to make sure that no information regarding the specific error is presented to the user, as this could be useful to an attacker to determine what is being validated for in the input. The major disadvantage of this approach is that the [user experience](https://www.sciencedirect.com/topics/computer-science/user-experience) is interrupted and any transaction in progress may be lost. You can mitigate this by additionally performing input validation at the client’s browser, to ensure that genuine users should not submit invalid data, but you cannot rely on this as a control because a malicious user can change what is ultimately submitted to the site.

Whichever approach you choose, ensure that you log that an input validation error has occurred in your application logs. This could be a valuable resource for you to use to investigate an actual or attempted break-in to your application.
# Blacklisting
**Blacklisting** is the practice of only rejecting input that is known to be bad. This commonly involves rejecting input that contains content that is specifically known to be malicious by looking through the content for a number of “known bad” characters, strings, or patterns. This approach is generally weaker than whitelist validation because the list of potentially bad characters is extremely large, and as such any list of bad content is likely to be large, slow to run through, incomplete, and difficult to keep up to date.

A common method of implementing a blacklist is also to use regular expressions, with a list of characters or strings to disallow, such as the following example:
```
‘|%| — |;|/\|\\\||\[|@|xp
```

In general, you should not use blacklisting in isolation, and you should use whitelisting if possible. However, in scenarios where you cannot use whitelisting, blacklisting can still provide a useful partial control. In these scenarios, however, it is recommended that you use blacklisting in conjunction with output encoding to ensure that input passed elsewhere (e.g., to the database) is subject to an additional check to ensure that it is correctly handled to prevent SQL injection.

Blacklisting attempts to check that given data does not contain “known bad” content. For example, a web application may block input that contains the exact text "SCRIPT" in order to help prevent XSS. However, this defense could be evaded with a lower case script tag or a script tag of mixed case.

## Whitelisting
Whitelist validation is the practice of only accepting input that is known to be good. This can involve validating compliance with the expected type, length or size, numeric range, or other format standards before accepting the input for further processing. 

For example, validating that an input value is a credit card number may involve validating that the input value contains only numbers, is between 13 and 16 digits long, and passes the business logic check of correctly passing the [Luhn formula](https://en.wikipedia.org/wiki/Luhn_algorithm) (the formula for calculating the validity of a number based on the last “check” digit of the card).

When using whitelist validation you should consider the following points:

- **Data type**: Is the data type correct? If the value is supposed to be numeric, is it numeric? If it is supposed to be a positive number, is it a negative number instead?
- **Data size**: If the data is a string, is it of the correct length? Is it less than the expected maximum length? If it is a binary blob, is it less than the maximum expected size? If it is numeric, is it of the correct size or accuracy? (For example, if an integer is expected, is the number that is passed too large to be an integer value?)
- **Data range**: If the data is numeric, is it in the expected numeric range for this type of data?
- **Data content**: Does the data look like the expected type of data? For example, does it satisfy the expected properties of a ZIP Code if it is supposed to be a ZIP Code? Does it contain only the expected character set for the data type expected? If a name value is submitted, only some punctuation (single quotes and character accents) would normally be expected, and other characters, such as the less than sign (<), would not be expected.

A common method of implementing content validation is to use regular expressions. Following is a simple example of a regular expression for validating a U.S. ZIP Code contained in a string:

> _**^\d{5}(-\d{4})?$**_

In this case, the regular expression matches both five-digit and five-digit + four-digit ZIP Codes as follows:

- ***^\d{5}***: Match exactly five numeric digits at the start of the string.
- ***(–\d{4})?***: Match the dash character plus exactly four digits either once (present) or not at all (not present).
- $: This would appear at the end of the string. If there is additional content at the end of the string, the regular expression will not match.

In general, **whitelist validation** is the more powerful of the two input validation approaches. It can, however, be difficult to implement in scenarios where there is complex input, or where the full set of possible inputs cannot be easily determined. Difficult examples may include applications that are localised in languages with large character sets (e.g., Unicode character sets such as the various Chinese and Japanese character sets). It is recommended that you use whitelist validation wherever possible, and then supplement it by using other controls such as output encoding to ensure that information that is then submitted elsewhere (such as to the database) is handled correctly.

# Designing an Input Validation and Handling Strategy

Input validation is a valuable tool for securing an application. However, it should be only part of a defense-in-depth strategy, with multiple layers of defense contributing to the application’s overall security. Here is an example of an input validation and handling strategy utilising
some of the solutions presented in this chapter:

- Whitelist input validation used at the application input layer to validate all user input as it is accepted by the application. The application allows only input that is in the expected form.
- Whitelist input validation also performed at the client’s browser. This is done to avoid a round trip to the server in case the user enters data that is unacceptable. You cannot rely on this as a security control, as all data from the user’s browser can be altered by an attacker.
- Blacklist and whitelist input validation present at a Web application firewall (WAF) layer (in the form of vulnerability “signatures” and “learned” behaviour) to provide intrusion detection/prevention capabilities and monitoring of application attacks.
- Parameterized statements used throughout the application to ensure that safe SQL execution is performed.
- Encoding used within the database to safely encode input when used in dynamic SQL.
- Data extracted from the database appropriately encoded before it is used. For example, data being displayed in the browser is encoded for cross-site scripting (XSS).