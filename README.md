# What is a Cookie

A concise guide to **Cookies**, covering what a cookie is, why we need it, all the main cookie options (`expires`, `Max-Age`, `path`, `Domain`, `Secure`, `HttpOnly`, `SameSite`), and how to create and delete a cookie.

## 📄 Contents

This guide covers:

- What a Cookie is
- Why you need a Cookie
- Cookie options:
  - **Lifetime:** `expires`, `Max-Age`
  - **Scope:** `path`, `Domain`
  - **Security:** `Secure`, `HttpOnly`, `SameSite`
- How to create and read a cookie
- How to delete a cookie
- Putting the options together
- Cookie options at a glance
- Key takeaways

## 🍪 What is a Cookie?

A cookie is a piece of data that is stored on your computer to be accessed by your browser. Cookies are saved as key/value pairs.

For example, you can create a cookie named `username`:

```javascript
document.cookie = "username=John";
```

## ❓ Why Do You Need a Cookie?

Cookies are used to remember information about the user profile (such as username). It basically involves two steps:

1. When a user visits a web page, the user profile can be stored in a cookie.
2. Next time the user visits the page, the cookie remembers the user profile.

## ⚙️ Cookie Options

### Lifetime

By default, a cookie is a **session cookie** and is generally removed when the browser session ends (browser behavior may vary). Use `expires` or `Max-Age` to keep it longer.

```javascript
// expires: a date in UTC (here: 7 days from now)
const d = new Date();
d.setDate(d.getDate() + 7);

document.cookie =
  `username=John; expires=${d.toUTCString()}`;

// Max-Age: lifetime in seconds
document.cookie = "username=John; Max-Age=604800";
```

> If both `Expires` and `Max-Age` are set, `Max-Age` wins. `Max-Age=0` deletes the cookie.

### Scope

By default, a cookie's path is derived from the URL path of the page that sets it. You can specify a different path using the `path` parameter, and share the cookie with subdomains using `Domain`.

```javascript
// Limit the cookie to a path
document.cookie = "username=John; path=/services";

// Share it across subdomains
document.cookie = "username=John; Domain=example.com";
```

> If `Domain` is omitted, the cookie is sent only to the exact host that set it.

### Security

| Option | What it does |
| --- | --- |
| **`Secure`** | Sends the cookie only over HTTPS (browsers make an exception for `localhost`). |
| **`HttpOnly`** | Hides the cookie from JavaScript, so `document.cookie` can't read it. Only the server can set it. |
| **`SameSite`** | Controls whether the cookie is sent on cross-site requests (helps against CSRF). Values: `Strict`, `Lax`, `None`. |

## 🗑️ Deleting a Cookie

Delete a cookie by setting its expiry date to a date in the past. No cookie value is needed.

```javascript
// Delete a cookie: set a past expiry date
document.cookie =
  "username=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/";

// Or expire it immediately with Max-Age
document.cookie = "username=; Max-Age=0; path=/";
```

> The `path` (and domain) must match the original cookie, or the browser won't delete it.

## 🔗 Putting It Together

**From JavaScript** (`HttpOnly` is not possible here):

```javascript
document.cookie =
  "theme=dark; Max-Age=604800; Path=/; Secure; SameSite=Lax";
```

**From the server** (best for login cookies):

```
Set-Cookie: sessionId=abc123;
  Max-Age=3600; Path=/;
  Secure; HttpOnly; SameSite=Strict
```

## 📚 Cookie Options at a Glance

| Option | Default Behavior | How to Change It |
| --- | --- | --- |
| **Lifetime** | Session cookie; removed at session end | `expires=<UTC date>` / `Max-Age=<sec>` |
| **Scope** | Path from URL; host-only domain | `path=/services`; `Domain=example.com` |
| **Security** | Sent over HTTP; readable by JS | `Secure`; `HttpOnly`; `SameSite=Lax` |
| **Format** | Saved as a key/value pair | `document.cookie = "username=John"` |
| **Delete** | Stays until it expires | Past expiry (or `Max-Age=0`) + same path |

## ✅ Key Takeaways

1. **Key/value data**: a cookie is a piece of data stored on your computer, saved as key/value pairs.
2. **Remembers the user**: cookies remember profile info, such as a username, the next time the user visits.
3. **Lifetime** (`expires` / `Max-Age`): by default it is a session cookie; set an expiry date or `Max-Age` to keep it longer.
4. **Scope** (`path` / `Domain`): the path comes from the page's URL by default; `Domain` shares it with subdomains.
5. **Security** (`Secure`, `HttpOnly`, `SameSite`): HTTPS only, hidden from JavaScript, and limited on cross-site requests.
6. **Deleting a cookie**: use a past expiry date (or `Max-Age=0`) with the same path as the original cookie.

## 📥 PDF

The complete guide is available in the PDFs below:

- **[What is a Cookie (English).pdf](./What_is_a_Cookie.pdf)**
- **[What is a Cookie (Persian).pdf](./What_is_a_Cookie_FA.pdf)**
