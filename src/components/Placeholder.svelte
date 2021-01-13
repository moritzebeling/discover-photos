<script>

    let columns = 4;
    let rows = 4;

</script>

<table width="100%">
    {#each (new Array( columns )) as item }
        <tr>
            {#each (new Array( rows )) as item }
                <td></td>
            {/each}
        </tr>
    {/each}
</table>

<style lang="scss">

    table {
        width: 100%;
        height: 100%;
    }
    tr {
        height: 1rem;
    }

    table tr:nth-child(odd) td:nth-child(even) {
        background: $white;
    }
    table tr:nth-child(even) td:nth-child(odd) {
        background: $white;
    }

</style>
