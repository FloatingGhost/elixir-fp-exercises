1. `h Elixir.at`
2. 

```elixir
defmodule Math do
  def square(n) when is_integer(n), do: n*n
end
```

```bash
iex
c "math.exs"
Math.square(5)
```

3. `?` implies the function returns a boolean. `!` implies the function can throw an exception.
4. Pipe passes the output of whatever is on the left of it as the first argument to the function on the right

that is to say, `x |> f()` is 100% equivalent to `f(x)`. This is useful when stringing together functions,
since the rather unweildy `f(g(h(i(a, c)), b))` can be rewritten 

```elixir
a
|> i(c)
|> h()
|> g(b)
|> f()
```

The benefit becomes more immediately obvious if i were to post this snippet

```elixir
def get_account(id, config) do
    config
    |> Map.get(:base_url)
    |> URI.parse()
    |> URI.merge("/api/v1/accounts/#{id}")
    |> URI.to_string()
    |> HTTPoison.get()
    |> case do
        {:ok, %HTTPoison.Response{status_code: 200, body: body}} ->
            handle_success(body)
        {:ok, resp} -> handle_failure(resp)
    end
end
```

5. `mix format`
6. `elem({"fake name", 1293}, 1)`
7. `[1] ++ [2]`
8. 
```elixir
head = hd [1,2,3]
[head | _tail ] = [1,2,3]
```

9. `%{1 => "one", what: "do you want", me: "to put here", aaaaa: :atomic, beep: "boop" }`
10. 


```elixir
x = %{a: "magical value"}
%{a: wew} = x
wew == "magical value"
```

11. They are fundamentally just different ways to represent the same data. A binary string is an arbitrary
list of bytes, which when interpreted in a certain way can be a string. i.e `<<72,101,110,108,111>>` is valid utf8.
A charlist is just a special case of an array - `[72,101,110,108,111]`. An array of integers can be interpreted
as a list of codepoints. Any possible charlist can be represented by a binary. Charlists only really exist
for using erlang libraries without elixir bindings - you won't use them very much. 

