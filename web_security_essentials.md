# Web Security Essentials
Open Web Application Security Project: http://owasp.org

# Basic Tips
- Don't run web server as root
- Restrict web server user to web files
- Finer grained permissions for database users
- Different DB users for read/write
- Force permissions for URLs - don't just put private files in statically served locations
- Limit information leak through errors - don't blindly dump exception data in 500 errors
- Keep your software stack updated!
- Log everything so you can trace an attack

# Password Protection
- Don't restrict password characters
- Minimum length is good, but don't restrict maximum
- Requiring mixed symbols can help, but makes passwords harder to deal with for users
- No plain text, 1-way hash, no MD% or SHA-1 - suggested to use bcrypt or scrypt if available (from crypto 101 class)
- Use libraries built for password hashing, don't try to invent your own
- 2FA/MFA provides an effective second layer of protection

# Filter Input/Escape Output
- Filter the data that comes in to ensure that it's what you expect
    - Simplifies security later
    - Provides security in depth (because it stops attacks from being stored on your systems)
    - Makes for cleaner data
- Escape the data going out to protect the user

- Validate: refuse data if it's invalid
    - Downside is that you end up not being flexible for possibly valid input.
- Sanitize: attempt to clean up data to make it valid
    - Downside is that the user may end up with something other than what they expected.

## SQL Injection
Un-filtered input from user could affect SQL query statements if it is unchecked. This can be handled by preparing statements separately from the input and then applying the input on executing the statement. This method forces the SQL parser to only parse SQL statements from the prepared statement and will not interpret the input parameters as part of the SQL language.

## Code Injection
Languages like PHP or JavaScript can evaluate code and run it, making code that contains those statements vulnerable to injection.

## Unchecked File Uploads
Check uploaded files to make sure they are what they are supposed to be. Image files should be image files.

## Command Injection
Code that can be injected to run in the shell. Each language has its own escaping functions to prevent this, but you have to use it.

# Session Hijacking
One user becoming another by taking over their session via impersonation.

## Ways to avoid
- Do not use URL query parameter for session ID
- Every time a user access level changes (login/logout), regenerate session ID
- Use anti-hijack measures:
    - Store unique information about the browser (as much as possible) - User agent string is probably the best you can do
    - Hash the unique browser data with a salt and a unique piece of data for the session and create a cookie with the data that can be checked later
    - On request check if the anti-hijack cookie exists and compare the contents with the same data saved in the session cookie - if it's the same, then the user is good, otherwise deploy countermeasures.

# Cross Site Scripting (XSS)
User sending data that can be executed as script (JavaScript). This can mostly be avoided by following the rules for filtering input and output.

## Reflected XSS
Directly echoing user provided content back to the user. User can put JavaScript code into a text input box and if it's included in the rendered HTML, the script code will run. This isn't really an effective form of attack because it requires either physical access to a user's browser or a really stupid/gullible user.

For generating data to be used by JavaScript, just use JSON! Don't generate JavaScript code!

## Stored XSS
Instead of directly input data from the user, the data is stored in your database. The outcome and solution is the same as reflected XSS, but it's more likely that it could be deployed by one user to affect other users, so the ramifications may be more dire.

## DOM XSS
JavaScript-only attack where user provided data is being used to render content without filtering.
- Can escape with a nasty string replacement function.
- Use the data properly - assign the data to the text/value of an element instead of trying to render HTML with JavaScript (which you shouldn't do anyway, especially if you're using something like AngularJS)

# CSRF - Cross Site Request Forgery
A user having the ability to forge or force a request on behalf of another user.
- Can be done with an `img` element with the `src` on another site (height and width must be non-zero)
- Can also be done with an actual AJAX POST - especially tricky with a hidden iframe containing the target site

Solved by generating a session token provided to the browser that has to be included as one of the input elements on the form submission. If a form POST is made without a token or with an invalid token, you can reject it.

# Clickjacking
Overlap an iframe on top of a form with the iframe opacity 0. The iframe is effectively hidden and when the user attempts to click on the button they see, they end up clicking on the button in the iframe instead.

Possible solution is to use the `X-Frame-Options` header set to `DENY` or `SAMEORIGIN`.
- `DENY` - Never allow the site to be inside an iframe
- `SAMEORIGIN` - Allows the site to be inside an iframe on the same domain

For browser's that don't support `X-Frame-Options`, you have to use hide your page's body first in `head` and then run a script that checks if the current site is inside an iframe and only if it's not, set `display` back to `block` for the body.

# Brute Force Attacks for Passwords
Two options to solve:
- CAPTCHA
- IP Rate Limiting
