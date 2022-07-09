# grafana-prometheus-node-js-example

# 🚀 Visualizing metrics from the Node JS application with Prometheus and Grafana 🚀

https://github.com/coding-to-music/grafana-prometheus-node-js-example

From / By Sergey Potekhin https://github.com/pavlovdog

https://github.com/pavlovdog/grafana-prometheus-node-js-example

https://sergeypotekhin.com/visualizing-data-from-the-node-js-app

Example of a Grafana dashboard, using data from Prometheus:

![Grafana screenshot](https://github.com/coding-to-music/grafana-prometheus-node-js-example/blob/main/images/example-dashboard.png?raw=true)

## Environment variables:

```java

```

## GitHub

```java
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/grafana-prometheus-node-js-example.git
git push -u origin main
```

# Visualizing metrics from the Node JS application with Prometheus and Grafana

## Run

```bash
docker-compose up -d
```

Then open the http://localhost:3000, login (admin:illchangeitanyway) and check out the results!

Full tutorial you can find in my blog - [https://sergeypotekhin.com/](http://sergeypotekhin.com/visualizing-data-from-the-node-js-app/?utm_source=github&utm_medium=readme&utm_campaign=repos).

See ya!

## Prometheus port has been changed to 9095 to avoid conflicts with existing use of the port

Prometheus port has been changed to 9095 to avoid conflicts with existing use of the port

## App metrics

```java
const client = require('prom-client');
const gaussian = require('gaussian');


function activeUsersPerCategoryMetric(registry) {
  const gauge = new client.Gauge({
    name: 'active_users',
    help: 'Amount of active users right now per category',
    registers: [registry],
    labelNames: [
      'category',
    ],
  });

  // To make data looks more
  const categoriesWithDistribution = [
    ['oil', 100, 30],
    ['wine', 200, 30],
    ['bread', 300, 30],
    ['butter', 400, 30],
  ];

  async function collectActiveUsers() {
    categoriesWithDistribution.map(async ([category, mean, variance]) => {
      gauge.set(
        { category },
        Math.floor(gaussian(mean, variance).ppf(Math.random())),
      );
    });
  }

  setInterval(collectActiveUsers, 5000);
}


module.exports = (registry) => {
  activeUsersPerCategoryMetric(registry);
};

```

## view the app metrics

http://localhost:9200/metrics

```
# HELP active_users Amount of active users right now per category
# TYPE active_users gauge
active_users{category="oil"} 101
active_users{category="wine"} 204
active_users{category="bread"} 298
active_users{category="butter"} 396
```
