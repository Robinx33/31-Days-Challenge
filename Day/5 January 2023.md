`5 January 2023`
## **Day 19 What I Have Learned**
***
## **Password Reset Token Issues**:
- Password Reset isssues are most caused by Weak Cryptography or Implemated Poorly and  can be easily figured out to takeover an account.
- Most of the applications provide the user’s with functionality to “Reset Password” via email
## **Attacks**:
1. Weak Cryptography in Password Reset Tokens 
- Always check randomness in password reset tokens. It is also a good idea to check password reset tokens against known schemes.
- Try to compare Two different Password Reset Links to see similarity.
- [More](https://infosecwriteups.com/weak-cryptography-in-password-reset-to-full-account-takeover-fc61c75b36b9).
2. Reusable Password Reset Tokens 
- Use the token once and try to re-use it again. 
- Request a new token and try if the old one is still active. 
- Check how long a token stays alive. If it's >1 day and is reusable, you may report it.
3. IDOR (ATO)
- In the password reset link, assume there is something like this: https://harshbothra.tech/reset?token=sometoken&user=harsh
- Try changing the value of the user parameter to the victim and see If the attack token can be used for resetting the victim's password. https://harshbothra.tech/reset?token=sometoken&user=victim.
4. Lack of Random Generation in Password Reset Token
- Request multiple passwords reset tokens. 
- If all the requested tokens are identical, it is confirmed that some Identifier is crypted to generate a password reset token. 
- Try guessing the crypto else still an issue.
5. Weak/Small Password Reset Token is used 
- If a password reset token used by the application is weak/small/guessable, it can be brute-forced.
6. Password Reset Token not Validated 
- Navigate to the password reset link and remove the token parameter or send only empty values. 
- Only keep the user identifier and change that to the victim user's identifier 
- See if it is possible to change the password.
7. Excessive Information in JWT Based Password Reset Token 
- If the password reset token is JWT Based, check for the following: 
a. If there is any excessive info, it may contain an old password (never seen but you never know)
b. Make sure that asymmetric algo is used.

## **Resources**:
- [Weak Cryptography in Password Reset](https://infosecwriteups.com/weak-cryptography-in-password-reset-to-full-account-takeover-fc61c75b36b9).

***
## **The End**