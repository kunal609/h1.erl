h1
=====

Library for simplifying interactions with the HackerOne API.

Build
-----

    $ rebar3 compile


Install
-------

Add to your dependencies in ```rebar.config```:

```erlang
{ deps, [
    { h1, { git, "git://github.com/wrren/h1.erl.git"} }
] }
```

Test
----

Copy ```config/test.config.example``` to ```config/test.config``` and fill in the values there, the 
included common test suite requires these configuration values in order to run.

```bash
rebar3 do compile, eunit, ct
```

Usage
-----

```erlang
Program = "program",                            %% Your Program Name (uber, riot, etc.)
Handle = h1:init( "token_id", "token_key" ),    %% Initialize a handle for use in requests
{ ok, Report } = h1:report( 12345, Handle ),    %% Retrieve the report with the specified ID

%% Find all reports created before September 16th, 2016 that have had a bounty awarded
{ ok, CreatedBefore } = h1:reports( [{ created_before, "2016-09-16T00:00:00Z" }, { bounty_awarded, true }], Program, Handle ).

%%     Available Filters:
%%
%%     program ([string()] | string())
%%     state ([string()] | string())
%%     id ([string()] | string())
%%     created_after (calendar:datetime() | string()) 
%%     created_before (calendar:datetime() | string())
%%     triaged_after (calendar:datetime() | string())
%%     triaged_before (calendar:datetime() | string())
%%     closed_after (calendar:datetime() | string())
%%     closed_before (calendar:datetime() | string())
%%     disclosed_after (calendar:datetime() | string())
%%     disclosed_before (calendar:datetime() | string())
%%     swag_awarded_after (calendar:datetime() | string())
%%     swag_awarded_before (calendar:datetime() | string())
%%     bounty_awarded_after (calendar:datetime() | string())
%%     bounty_awarded_before (calendar:datetime() | string())
%%     last_reporter_activity_after (calendar:datetime() | string())
%%     last_reporter_activity_before (calendar:datetime() | string())
%%     last_program_activity_after (calendar:datetime() | string())
%%     last_program_activity_before (calendar:datetime() | string())
%%     first_program_activity_after (calendar:datetime() | string())
%%     first_program_activity_before (calendar:datetime() | string())
%%     last_activity_after (calendar:datetime() | string())
%%     last_activity_before (calendar:datetime() | string())
%%     triaged (boolean())
%%     closed (boolean())        
%%     disclosed (boolean())       
%%     swag_awarded (boolean())        
%%     bounty_awarded (boolean())        
%%     first_program_activity (boolean())  

```

