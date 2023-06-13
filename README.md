# Resend with Phoenix

This example shows how to use Resend with [Phoenix](https://phoenixframework.org/).

Created using Phoenix [v1.7.3](https://github.com/phoenixframework/phoenix/releases/tag/v1.7.3).

## Prerequisites

To get the most out of this guide, you’ll need to:

* [Create an API key](https://resend.com/api-keys)
* [Verify your domain](https://resend.com/domains)

## Setup

Add `:resend` to your project deps:

```elixir
  defp deps do
    [
      {:resend, "~> 0.2"},
      # ...
    ]
  end
```

Once added, fetch the new dependency with `mix deps.get`.

Configure your `App.Mailer` to use the Resend Swoosh adapter by adding the following code
to [`config/runtime.exs`](./config/runtime.exs):

```elixir
config :app, App.Mailer,
  adapter: Resend.Swoosh.Adapter,
  api_key: System.fetch_env!("RESEND_KEY") || "re_123456789"
```

Replace `re_123456789` with your own API key, or fetch it from the environment.

To start your Phoenix server:

  * Run `mix setup` to install and setup dependencies
  * Start Phoenix endpoint with `mix phx.server` or inside IEx with `iex -S mix phx.server`

Now you can visit [`localhost:4000`](http://localhost:4000) from your browser.

If running in `iex`, you can send an email by invoking this function, as an example:

```elixir
iex(1)> App.Users.UserNotifier.deliver_confirmation_instructions("recipient@example.com", "example.com")
```

Alternatively, try creating an account at [`localhost:4000/users/log_in`](http://localhost:4000) to
receive a welcome email.

See [`lib/app/users/user_notifier.ex`](./lib/app/users/user_notifier.ex) for other examples of delivering emails.

## Use with Phx.Gen.Auth

The above setup works as-is with code generated from [phx_gen_auth](https://hexdocs.pm/phoenix/mix_phx_gen_auth.html),
Phoenix Framework's built-in auth generator, as demonstrated in this example repo.

## Learn more

  * Official website: https://www.phoenixframework.org/
  * Guides: https://hexdocs.pm/phoenix/overview.html
  * Docs: https://hexdocs.pm/phoenix
  * Forum: https://elixirforum.com/c/phoenix-forum
  * Source: https://github.com/phoenixframework/phoenix

## License

MIT License