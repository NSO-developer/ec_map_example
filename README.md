## Example transform package using genet

This is an example package that uses ec_genet to transform between two data
models.  How to use it:

   * create an initial ncs project (e.g. `ncs-project create example`)

   * add `ec_genet` and `ec_map_example` as project's remote packages (in
     `project-meta-data.xml`) like this:

    ```
     <package>
      <name>ec_genet</name>
      <git>
        <repo>ssh://git@github.com/NSO-developer/genet.git</repo>
      </git>
    </package>
    <package>
      <name>ec_map_example</name>
      <git>
        <repo>ssh://git@github.com/NSO-developer/ec_map_example.git</repo>
      </git>
    </package>
    ```

   * run `ncs-project update`

   * compile the project `make all`

   * start ncs
