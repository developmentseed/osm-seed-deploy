### Minimal Example for an osm-seed deployment repository

The recommended way to install osm-seed is to use the published Helm chart.

While you can use the Helm command line utility to directly install the Chart onto your Kubernetes cluster, we **strongly** recommend following a pattern to create a repository for your deployment.


### Basic Install Instructions:

This assumes you have Helm installed and `kubectl` configured to talk to your Kubernetes cluster.

Fork this repository. Then, visit https://github.com/developmentseed/osm-seed-chart/tree/gh-pages and find the latest published chart (or the version you wish to install), and replace the version number specified in osmseed/requirements.yaml.

Run `helm dependencies update` or `helm dep up` in the `osmseed/` folder. This will download the osm-seed chart into a `charts/` folder.

Then, if you wish to just test the install on a local `minikube` setup without any custom values, you can simply run `helm install <name> osmseed/` to install.

You will likely want to create custom values to customize your install, specify your cloud provider, etc. You can copy over the default `values.yaml` from the osm-seed repository: https://github.com/developmentseed/osm-seed and make changes to suit your setup. You can then run:

    helm install -f values.yaml <name> osmseed/


### Custom Installs

In most real-world setups, you will likely want to modify some containers, or maybe add additional containers not included in osm-seed.

To over-ride or add any Kubernetes templates, create a `templates/` folder in `osmseed/` and you can over-ride templates specified in the main osm-seed chart, or add your own.

If you need to over-ride the Docker images that come with the upstream osm-seed or add your own images, we recommend using `chartpress`: create a `chartpress.yaml` file in the root of this repository, and use the `chartpress` command to manage builds and versioning, ideally using automated CI. You can follow the same structure as used by osm-seed for the chartpress yaml and CI config.
