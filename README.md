# Zlibrary-API

Unofficial Zlibrary API for Python. No need for Libraries, just copy ```Zlibrary.py``` file to your project directory, one File can handle all your requests.

Only dependency is ```requests``` you can install it using 

```
pip install requests
```

---

# Documentation

## Importing
```
from Zlibrary import Zlibrary
```

## Logging in
It is recommended to use `remix_userid` and `remix_userkey` instead of `email` and `password` to login. you can get the said values from browser cookies or [login once using this library](#Guide) and then use the values in future.

* ### While creating Object
```
Z = Zlibrary(email="xxx@mail.com", password="password") # using mail and password

# OR

Z = Zlibrary(remix_userid="12345", remix_userkey="abcdef") # using remix id and keys
```
* ### After Object creation
```
Z = Zlibrary()

Z.login(email="xxx@mail.com", password="password") # using mail and password

# OR

Z.loginWithToken(remix_userid="12345", remix_userkey="abcdef") # using remix id and keys
```

## Availabale Methods

```
getProfile() -> dict[str, str]

getMostPopular(switch_language: str = None) -> dict[str, str]

getRecently() -> dict[str, str]

getUserRecommended() -> dict[str, str]

deleteUserBook(bookid: [int, str]) -> dict[str, str]

unsaveUserBook(bookid: [int, str]) -> dict[str, str]

getBookForamt(bookid: [int, str], hashid: str) -> dict[str, str]

getDonations() -> dict[str, str]

getUserDownloaded(order: str = None, page: int = None, limit: int = None) -> dict[str, str]

getExtensions() -> dict[str, str]

getDomains() -> dict[str, str]

getLanguages() -> dict[str, str]

getPlans(switch_language: str = None) -> dict[str, str]

getUserSaved(order: str = None, page: int = None, limit: int = None) -> dict[str, str]

getInfo(switch_language: str = None) -> dict[str, str]

hideBanner() -> dict[str, str]

recoverPassword(email: str) -> dict[str, str]

makeRegistration(email: str, password: str, name: str) -> dict[str, str]

resendConfirmation() -> dict[str, str]

saveBook(bookid: [int, str]) -> dict[str, str]

sendTo(bookid: [int, str], hashid: str, totype: str) -> dict[str, str]

getBookInfo(bookid: [int, str], hashid: str, switch_language: str = None) -> dict[str, str]

getSimilar(bookid: [int, str], hashid: str) -> dict[str, str]

makeTokenSigin(name: str, id_token: str) -> dict[str, str]

updateInfo(email: str = None, password: str = None, name: str = None, kindle_email: str = None) -> dict[str, str]

search(message: str = None, yearFrom: int = None, yearTo: int = None, languages: str = None, extensions: str = None, order: str = None, page: int = None, limit: int = None) -> dict[str, str]

getImage(book: dict[str, str]) -> requests.Response.content

downloadBook(book: dict[str, str]) -> (str, requests.Response.content)

isLoggedIn -> bool

send_code(self, email: str, password: str, name: str) -> dict[str, str]

verify_code(self, email: str, password: str, name: str, code: str) -> dict[str, str]
```

---

# Examples

* ### Handling Image
```
from Zlibrary import Zlibrary

# Create Zlibrary object and login
Z = Zlibrary(email="xxx@mail.com", password="password")

# Search for books
results = Z.search(message='The Great Gatsby')

# Getting image content
imgcontent = Z.getImage(results["books"][0])

# Writting image content to a file
with open("img.jpg", "wb") as imgfile:
    imgfile.write(imgcontent)
```

* ### Downloading a Book
```
from Zlibrary import Zlibrary

# Create Zlibrary object and login
Z = Zlibrary(email="xxx@mail.com", password="password")

# Get most popular books
most_popular = Z.getMostPopular()

# Downloading a book
filename, filecontent = Z.downloadBook(most_popular["books"][0])

# Writting file content to a file
with open(filename, "wb") as bookfile:
    bookfile.write(filecontent)
```

---

# Guide

* ### To get REMIX values from email and password (Recommended)

```
from Zlibrary import Zlibrary

Z = Zlibrary(email="abc@mail.com", password="xxxxxxxx")
user_profile = Z.getProfile()["user"]

print("Remix User ID:", user_profile["id"])
print("Remix User Key:", user_profile["remix_userkey"])
```

---

# Credits for Endpoints

* [zlibrary-eapi-documentation](https://github.com/baroxyton/zlibrary-eapi-documentation) by baroxyton
