# Indirect Prompt Injection

## 1. Vulnerability

**Indirect Prompt Injection**

Indirect prompt injection occurs when an attacker places malicious instructions in data that an LLM later processes as part of its normal operation. If the application does not properly separate trusted instructions from untrusted external content, the LLM may follow the injected instructions.

## 2. Objective

Inject a malicious prompt into a product review and cause the LLM to execute the `delete_account` function on another user's account.

## 3. Exploitation

1. Register and log in using the email address provided in the lab instance.
2. Write a review for the **Lightweight "l33t" Leather Jacket** containing an indirect prompt injection instructing the LLM to delete the user's account using the `delete_account` function.
3. Change the user associated with the same email address from the attacker-controlled account to **carlos**.
4. Ask the LLM to provide the product review for the leather jacket. The LLM processes the previously stored malicious review as part of the product information.
5. The injected instructions are interpreted by the LLM as instructions and cause it to invoke the `delete_account` function.
6. Since the email is now associated with **carlos**, the function deletes Carlos's account and the lab is successfully completed.

## 4. Impact

Indirect prompt injection can allow attackers to:

* Manipulate an LLM through stored or externally supplied content.
* Cause the LLM to perform unintended actions.
* Abuse functions and APIs available to the LLM.
* Potentially access, modify, or delete another user's data.

The impact depends on the privileges and functions available to the LLM.

## 5. Remediation

* Treat all external content processed by the LLM as **untrusted input**.
* Clearly separate system instructions from user-controlled data.
* Do not allow LLM-generated instructions to directly trigger sensitive actions.
* Require independent authorization before executing sensitive functions.
* Apply the **principle of least privilege** to LLM tools and functions.
* Implement confirmation and validation mechanisms for destructive actions.

## 6. Key Takeaway

**Never assume that content retrieved by an LLM is trustworthy.** An attacker can plant malicious instructions in seemingly harmless content, which may later be processed by the LLM and cause unintended actions in another user's context.
