# Section-driven docs example

This repo provides an illustration of what a section-driven docs repo *could* look like:

* `section.yml` files define sections
* Anything "under" a `section.yml` is inside that same section _unless_ another `section.yml` defines a new nested section inside. For example, there's a section called `Kubernetes administration` as defined by [`./docs/admin/kubernetes/section.yml`](./docs/admin/kubernetes/section.yml) that contains the doc in [`./docs/admin/kubernetes/helm/deployment.md`](./docs/admin/kubernetes/helm/deployment.md) even though it's in a subdirectory (because there's no `section.yml` in the `helm` subdirectory).
* Sections are potentially infinitely nestable.

Ideally, this `docs` directory would produce TypeScript objects like this:

```ts
type Page = {
  title: string;
  path: string;
  weight: number;
  body: string;
};

type Section = {
  title: string;
  metadata: object;
  weight: number;
  pages?: Page[];
  sections?: Section[];
};

const docs: Section[] = [
  {
    title: "Documentation",
    metadata: {
      icon: "document"
    },
    pages: [
      {
        title: "Documentation",
        path: "index.md",
        weight: 1,
        body: "Welcome to the Fluffybird docs!"
      },
      {
        title: "About Fluffybird",
        path: "about.md",
        weight: 2,
        body: "..."
      }
    ],
    sections: [
      {
        title: "Installation",
        metadata: {
          icon: "floppydisk"
        },
        weight: 1,
        pages: [
          {
            title: "Installing Fluffybird",
            path: "installation/index.md",
            weight: 1,
            body: "..."
          },
          {
            title: "macOS",
            path: "installation/macos.md",
            weight: 2,
            body: "..."
          },
          {
            title: "Linux",
            path: "installation/linux.md",
            weight: 3,
            body: "..."
          }
        ]
      },
      {
        title: "Administration",
        metadata: {
          icon: "wrench"
        },
        weight: 2,
        pages: [
          {
            title: "Administration",
            path: "admin/index.md",
            weight: 1,
            body: "..."
          },
          {
            title: "Command-line interface",
            path: "admin/cli.md",
            weight: 2,
            body: "..."
          }
        ],
        sections: [
          {
            title: "Kubernetes administration",
            metadata: {
              icon: "kubernetes"
            },
            weight: 1,
            pages: [
              {
                title: "Kubernetes admin",
                path: "admin/kubernetes/index.md",
                weight: 1,
                body: "..."
              },
              {
                title: "Scaling Fluffybird on Kubernetes",
                path: "admin/kubernetes/scaling.md",
                weight: 2,
                body: "..."
              },
              {
                title: "Deploying using Helm",
                path: "admin/kubernetes/helm/deployment.md",
                weight: 3,
                body: "..."
              }
            ]
          }
        ]
      }
    ]
  }
];
```