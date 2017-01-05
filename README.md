This is an example package that uses ec_genet.  How to use it:

   * create an initial ncs project (e.g. `ncs-project create example`)
   * add `ec_genet` and `ec_map_example` as project's remote packages (in
     `project-meta-data.xml`)
   * run `ncs-project update`
   * compile the two packages `make -C packages/ec_genet` and
     `make -C packages/ec_map_example`
   * start ncs
