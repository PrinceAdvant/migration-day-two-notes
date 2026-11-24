# Questions to answer before choosing a Dokploy plan

Dokploy can be run free on your own server or used through a hosted control plane that manages your servers for a fee. Picking between them is less about price and more about who carries which risk.

Ask yourself four questions. Who patches the control plane? Self-hosted means you apply updates and handle a broken upgrade. How many servers will you connect in a year? Per server pricing grows with your footprint. What happens to running apps if the control plane is unreachable? Ideally they keep serving and only deploys pause. Can you export your configuration if you leave?

Also consider the server the control plane runs on. Self-hosting it on the same machine as your apps saves money, but a resource spike in one app can make the dashboard slow exactly when you need it.

Write down your answers before comparing numbers. Teams that skip this step tend to pick on headline price and move again later. The current plans are summarised in [Dokploy pricing, cloud versus self-hosted](https://peon.sh/blogs/dokploy-pricing-2026).
