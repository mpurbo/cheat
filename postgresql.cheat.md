# PostgreSQL Cheat Sheet

## Database Administration

<table>
    <tr><th>Purpose</th><th>Command</th></tr>
    <tr>
        <td>Create UTF-8 Japanese db with a specific owner.</td>
        <td><code>createdb -U postgres -O [owner] -E UTF8 -l ja_JP.UTF-8 -T template0 [db-name]</code></td>
    </tr>
    <tr>
        <td>Dump a UTF-8 database.</td>
        <td><code>pg_dump -i -U postgres -F c -b -v -E UTF8 -f "[dump-name]" [db-name]</code></td>
    </tr>
    <tr>
        <td>Restore a database.</td>
        <td><code>pg_restore -U postgres -d [db-name] [dump-name]</code></td>
    </tr>
    <tr>
        <td>Copy an idle database.</td>
        <td><code>createdb -O [ownername] -T [originaldb] [newdb]</code></td>
    </tr>
    <tr>
        <td>Copy a live database (dump, create, restore).</td>
        <td>
            <pre>
            pg_dump -i -U postgres -F c -b -v -E UTF8 -f "[dump-name]” [src-db-name]
            createdb -U postgres -O [owner] -E UTF8 -l ja_JP.UTF-8 -T template0 [target-db-name]
            pg_restore -U postgres -d [db-name] [dump-name]
            </pre>
        </td>
    </tr>
    <tr>
        <td>Change database owner.</td>
        <td><code>sql> alter database "[db-name]" owner to [new-owner]</code></td>
    </tr>
    <tr>
        <td>Running psql in Windows using UTF-8</td>
        <td><code>
            SET PGCLIENTENCODING=utf-8<br/>
            chcp 65001<br/>
            psql -h localhost -U postgres
        </code></td>
    </tr>    
</table>    

