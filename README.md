# ELOGGER

elogger is a disk based, file wrapping, error_logger.

''elogger.erl'' is identical to the ''logger.erl'' module from jungerl.
It has been renamed and put at github for convenient usage by
other Erlang github project.

To set it up: add it it as a git submodule and make sure the
Erlang path is including its `ebin` directory. Then start it
from your supervisor. Example:

    server(Name, Type) ->
        server(Name, Type, 2000).
    
    server(Name, Type, Shutdown) ->
        {Name, {Name, start_link, []}, permanent, Shutdown, Type, [Name]}.
    
    worker(Name) -> server(Name, worker).
    
    init([]) ->
    
        Elogger = worker(elogger),
    
        {ok,{{one_for_one ,0,1},
             [Elogger
             ]}}.

Use the following configurations parameters in your `.app` files
to control the name, size and number of logfiles.

    {env, [
        ...
        {nolog, false},
        {errlog_type, error}, % all : also progress reports
        {error_logger_mf_file, "/var/log/redhot/redhot"},
        {error_logger_mf_maxbytes, 500000},
        {error_logger_mf_maxfiles, 5},
        ...

Good luck!

--Tobbe
