# memail -- A SMTP-based Mass Mail Python Script

This is a Python script that allows you to send mass emails with a message template, a CSV list of recipients, and optional attachments using SMTP protocol.

## Requirement
- Python 3.2+

## Installation

To use this script, you will need Python 3 installed on your system. You can download Python 3 from the [official website](https://www.python.org/downloads/).

To download the code, you can either download the ZIP from Github or using `git clone`.

## Usage
```shell
./memail [-h] [-a [ATTACH ...]] [TEMPLATE] [RECIPIENT]
```
Positional arguments
:
- **`TEMPLATE`**
: The txt file path of email body template.
- **`RECIPIENT`**
: The csv file path of recipients information, including the email and things you want to replace.

Optional arguments
:
- **`-h`, `--help`**
: Show the help message and exit.
- **`-a [ATTACHMENTS...], --attachments [ATTACHMENTS...]`**
: The name of the files you want to attach to the email, separated by a space.

## Example
```shell
./memail template.txt recipients.csv -a resume.pdf slide.pptx
```

## Input
Add necessary information here. If you don't know the smtp things, I will discuss it later.
```python
# Setup connection
smtp_server = "smtp_server_here"
smtp_port = "smtp_server_port_here"
smtp_username = "your_email_here"
smtp_password = os.environ['EMAIL_PASSWORD']
```
### Template
The email templates is a txt file with the following structure
:
```
Subject: Your email subject line here

Your email body here. You can use placeholders inside curly braces to replace them with the corresponding recipient's information. For example:

Dear {name},

This is a test email.

{university}
```
The first line is email subject. The content after first space will be the actual subject in the email. The remaining in the file is the email body.

Subject and body must be separated by one line. 

You can use placeholders inside curly braces to replace them with the corresponding recipient's information. The name inside the curly braces must match the column names in the CSV file. 

**You must use "email" and "name" to store recipient's email and name respectively.**

### Recipient
The CSV file must have a header row with the column names. Each row below the header represents a recipient's information.

For example
```
email,name,university
joe@example.com,joe,MIT
josie@example.com,josie,MIT
```

### Attachment

If you want to attach files to the email, you can pass their file paths as optional arguments separated by space after the recipient's file path.
> For Gmail users, Gmail doesn't allow attaching certain types of file. See more at [link](https://support.google.com/mail/?p=BlockedMessage).

## Setup SMTP server

If you are using email servers provide by companies like Google and Microsoft, you can google "how to setup {provider} smtp server" and follow the instruction.

If you are hardcore and using your own server's smtp service, I believe there is no need to talk about the instruction here.

### Password

You can setup your password by pasting to here
```python
smtp_password = "password_here"
```
If you are worried about security issue, you can export your password as an environment variable and do
```python
smtp_password = os.environ['EMAIL_PASSWORD']
```
> To export your password as an environment variable, if you are a mac user, run `export EMAIL_PASSWORD=your_password_here`. If you are a windows user, in your cmd, run `set SMTP_PASSWORD=mypassword`. (I am not a windows user. I hope this works.) If you are linux user, you should know the answer.

> For Gmail users, if you setup two-step verification, you need to generate an app password. You can find the detail [here](https://support.google.com/accounts/answer/185833?hl=en).

## Output
The script will send an email to each recipient using the SMTP protocol. If script send the email successfully, it will print the recipient's name to standard output. If there are any errors, the script will display an error message and exit.

## License
This project is licensed under the terms of the GNU General Public License v3.0 license.