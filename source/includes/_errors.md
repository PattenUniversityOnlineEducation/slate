# Errors

<aside class="notice">
This error section is stored in a separate file in <code>includes/_errors.md</code>. Slate allows you to optionally separate out your docs into many files...just save them to the <code>includes</code> folder and add them to the top of your <code>index.md</code>'s frontmatter. Files are included in the order listed.
</aside>

The Kittn API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- The resource requested is prohibited.
404 | Not Found -- The specified url could not be found.
405 | Method Not Allowed -- You tried to access a record with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
410 | Gone -- The record requested has not found in our database.
418 | Duplicate -- The record inserted has duplicate in our databse.
429 | Too Many Requests -- You're requesting too often! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
