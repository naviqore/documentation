# Client and Viewer

To demonstrate potential applications of our public transit service, we developed two Python packages.

## Client

The `public-transit-client` package was created to encapsulate the entire interaction with the Spring REST API, offering
pythonic functions and typed class objects for both request and response parameters. This package was built
using `poetry` and published to [PyPI](https://pypi.org/project/public-transit-client/), adhering to best practices,
including the inclusion of the `py.typed` file to support type hinting. The client is designed for both frontend
applications that integrate with the routing service and researchers who need to perform bulk routing requests directly
from Python without relying on a graphical user interface.

## Viewer

The second package, `public-transit-viewer`, is a mockup frontend application built using Streamlit, an open-source
Python framework designed for quickly building and deploying data-driven web applications with minimal effort. It
leverages the `public-transit-client` package to communicate with the Java-based public transit service. The viewer
provides a graphical interface to easily request connections and visualize results, making it useful for both
demonstration and debugging purposes. The viewer is published as image on
the [GitHub Container Registry](https://github.com/naviqore/public-transit-viewer/pkgs/container/public-transit-viewer)
for easy deployment.

While Streamlit allowed us to rapidly develop the application, its limited potential for customization and linear,
non-modular code structure makes it less ideal for a fully custom, branded frontend. For projects requiring a more
powerful and customizable user interface, we would recommend using a JavaScript framework. However, given the objectives
of this study, Streamlit's simplicity and rapid development capabilities made it an adequate choice for our needs.
