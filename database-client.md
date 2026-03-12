Neovim Database Client Setup (CLI Alternative to DataGrip)

This guide explains how to use Neovim with LazyVim as a database client similar to DataGrip.
Using the vim-dadbod ecosystem, you can connect to databases, run SQL queries, browse schemas, and view results directly inside Neovim.

This setup is ideal for developers who prefer a terminal-based workflow.

⸻

Tools

Core plugins:
	•	vim-dadbod
	•	vim-dadbod-ui
	•	vim-dadbod-completion

Optional CLI tools:
	•	pgcli (PostgreSQL)
	•	mycli (MySQL / MariaDB)
	•	usql (multi-database)

⸻

	1.	Install Plugins (LazyVim)

⸻

Create the plugin configuration file:

~/.config/nvim/lua/plugins/database.lua

Add the following configuration:

return {
{
“tpope/vim-dadbod”,
},
{
“kristijanhusak/vim-dadbod-ui”,
dependencies = {
“tpope/vim-dadbod”,
“kristijanhusak/vim-dadbod-completion”,
},
cmd = {
“DBUI”,
“DBUIToggle”,
“DBUIAddConnection”,
“DBUIFindBuffer”,
},
},
}

Install plugins:

:Lazy sync

Restart Neovim after installation.

⸻

	2.	Open Database UI

⸻

Run the following command inside Neovim:

:DBUI

This opens a sidebar showing:
	•	database connections
	•	schemas
	•	tables
	•	views
	•	indexes

You can browse database structures similar to DataGrip.

⸻

	3.	Add Database Connection

⸻

Run:

:DBUIAddConnection

Examples:

PostgreSQL:

postgres://user:password@localhost:5432/mydb

MySQL:

mysql://user:password@localhost:3306/mydb

SQLite:

sqlite:./database.db

Connections will appear in the DBUI explorer.

⸻

	4.	Running SQL Queries

⸻

Create a SQL file:

queries.sql

Example query:

SELECT *
FROM users
LIMIT 10;

Run the query inside Neovim:

:DB

Results will appear in a new buffer.

⸻

	5.	Autocompletion

⸻

With vim-dadbod-completion, Neovim provides:
	•	table name completion
	•	column name completion
	•	schema completion

This makes SQL development faster.

⸻

	6.	Example Workflow

⸻

Typical terminal workflow:

tmux
├─ nvim (code + SQL queries)
├─ database CLI
└─ logs

Inside Neovim you can:
	•	edit backend code
	•	run SQL queries
	•	inspect results
	•	browse database schemas

⸻

	7.	Optional CLI Database Clients

⸻

You can combine Neovim with CLI database clients.

PostgreSQL:

Install:

brew install pgcli

Run:

pgcli postgres://user@localhost/db

MySQL / MariaDB:

Install:

brew install mycli

Run:

mycli mysql://user@localhost/db

Multi-database client:

Install:

brew install usql

Run:

usql postgres://user:pass@localhost/db

⸻

	8.	Recommended Terminal Developer Stack

⸻

Many terminal-focused developers use:

tmux
├─ nvim
├─ pgcli
├─ httpie
└─ logs

This replaces heavy GUI tools like:
	•	DataGrip
	•	Postman
	•	other database GUI clients

⸻

Conclusion

Using Neovim with the vim-dadbod ecosystem turns your editor into a powerful database client.

Benefits:
	•	lightweight
	•	keyboard-driven
	•	terminal-friendly
	•	integrates with development workflow
	•	no heavy GUI tools required
