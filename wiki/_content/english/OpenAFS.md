From [Wikipedia:OpenAFS](https://en.wikipedia.org/wiki/OpenAFS "wikipedia:OpenAFS"):

	[OpenAFS](https://www.openafs.org/) is an open source implementation of the Andrew distributed file system (AFS).

AFS is a distributed filesystem product, pioneered at Carnegie Mellon University and supported and developed as a product by Transarc Corporation (now IBM Pittsburgh Labs). It offers a client-server architecture for federated file sharing and replicated read-only content distribution, providing location independence, scalability, security, and transparent migration capabilities. AFS is available for a broad range of heterogeneous systems including UNIX, Linux, MacOS X, and Microsoft Windows.

IBM branched the source of the AFS product, and made a copy of the source available for community development and maintenance. They called the release OpenAFS.

This page describes only the client side.

## Contents

*   [1 Client installation](#Client_installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 aklog: a pioctl failed while obtaining tokens for cell ...](#aklog:_a_pioctl_failed_while_obtaining_tokens_for_cell_...)
*   [3 See also](#See_also)

## Client installation

Install openafs client with the [openafs](https://aur.archlinux.org/packages/openafs/) and [openafs-modules](https://aur.archlinux.org/packages/openafs-modules/) packages.

Edit `/etc/openafs/ThisCell` and put default cell there. You can check for the cells in `/etc/openafs/CellServDB`.

[Start](/index.php/Start "Start") the `openafs-client` service.

## Troubleshooting

### aklog: a pioctl failed while obtaining tokens for cell ...

Your afs client is probably not running. Start it as described in [#Client installation](#Client_installation).

## See also

*   Official site [https://www.openafs.org/](https://www.openafs.org/)