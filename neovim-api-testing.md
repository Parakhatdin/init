:::

Advanced API Testing Workflow in Neovim (Postman Replacement)

This document describes a professional workflow for API development using Neovim + LazyVim instead of GUI tools like Postman.

The goal is to keep everything terminal-based, reproducible, and version controlled.

⸻

Overview

This workflow includes:
	•	.http files for API requests
	•	environment variables (.env style)
	•	request collections stored in Git
	•	CLI testing tools
	•	CI-ready API tests

Benefits:
	•	API tests can run locally or in CI
	•	No GUI dependency
	•	Everything stored as plain text

⸻

Tools

Core tools:
	•	Neovim
	•	LazyVim
	•	rest.nvim

Optional tools:
	•	HTTPie
	•	Hurl
	•	curl

⸻

1. Install Required Neovim Plugin

Create plugin file:

~/.config/nvim/lua/plugins/rest.lua

Configuration:

return {
  "rest-nvim/rest.nvim",
  dependencies = { "nvim-lua/plenary.nvim" },
  config = function()
    require("rest-nvim").setup({
      result_split_horizontal = false,
      result_split_in_place = false,
      skip_ssl_verification = false,
      encode_url = true,
      highlight = {
        enabled = true,
      },
    })
  end,
}

Run:

:Lazy sync


⸻

2. Project Structure

Recommended API testing structure:

project-root
│
├─ api/
│   ├─ environments/
│   │   ├─ dev.env
│   │   ├─ staging.env
│   │   └─ production.env
│   │
│   ├─ auth.http
│   ├─ users.http
│   └─ payments.http
│
└─ src/

Advantages:
	•	organized API requests
	•	environment separation
	•	easy team collaboration

⸻

3. Environment Files

Example:

api/environments/dev.env

Example content:

BASE_URL=https://dev-api.example.com
TOKEN=your-dev-token

Production example:

BASE_URL=https://api.example.com
TOKEN=prod-token


⸻

4. HTTP Request Files

Example file:

api/users.http

Example content:

@baseUrl = https://jsonplaceholder.typicode.com

### Get User
GET {{baseUrl}}/users/1

### List Users
GET {{baseUrl}}/users

### Create User
POST {{baseUrl}}/users
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com"
}


⸻

5. Using Authentication

Bearer token example:

GET {{baseUrl}}/users
Authorization: Bearer {{TOKEN}}

Basic authentication example:

GET {{baseUrl}}/users
Authorization: Basic username:password


⸻

6. Running Requests in Neovim

Place the cursor inside a request and execute:

:Rest run

Response includes:
	•	status code
	•	headers
	•	JSON formatted response body

⸻

7. Organizing Requests with Sections

You can separate requests with ###.

Example:

### Login
POST {{baseUrl}}/auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "password"
}

### Get Profile
GET {{baseUrl}}/users/me
Authorization: Bearer {{TOKEN}}

This behaves similarly to Postman collections.

⸻

8. CLI Testing with HTTPie

Install:

brew install httpie

Example requests:

http GET https://api.example.com/users

POST example:

http POST https://api.example.com/users name=John email=john@example.com

Advantages:
	•	readable syntax
	•	colored output
	•	easy debugging

⸻

9. API Testing with Hurl

Install:

brew install hurl

Example test file:

tests/users.hurl

Example content:

GET https://api.example.com/users
HTTP 200

Run tests:

hurl tests/users.hurl

This makes API tests CI compatible.

⸻

10. CI/CD Integration Example

Example CI command:

hurl tests/*.hurl

If any request fails, the CI pipeline fails.

This enables automated API testing.

⸻

11. Advantages Over Postman

Feature	This Workflow	Postman
Version control	Yes	Limited
Works in terminal	Yes	No
CI integration	Native	Complex
Plain text requests	Yes	No
Lightweight	Yes	No


⸻

12. Recommended Developer Workflow

Typical daily workflow:
	1.	Write API request in .http
	2.	Run request inside Neovim
	3.	Debug with HTTPie if needed
	4.	Add API tests with Hurl
	5.	Commit request files to repository

⸻

Conclusion

This setup transforms Neovim into a powerful API development environment.

Advantages:
	•	no GUI dependency
	•	fully scriptable
	•	version-controlled API testing
	•	CI-ready

It is widely used by backend developers who prefer terminal-first workflows.
:::
