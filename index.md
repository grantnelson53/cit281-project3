## Project 3

In this Project, we used our knowledge of Fastify and code modules to count coins 

### Source Code

    // Require the Fastify framework and instantiate it
    const fastify = require("fastify")();
    const fs = require("fs");
    import { coinCount } from './p3-module.js';

    // Handle GET verb for / route using Fastify
    // Note use of "chain" dot notation syntax

    fastify.get("/", (request, reply) => {
        fs.readFile("/index.html", (err, data) => {reply.send(data)});
      reply
        .code(200)
        .header("Content-Type", "text/html; charset=utf-8")
        //.send(documents / 281 / p3 / index.html);
        .send(__dirname + "/index.html");
    });

    fastify.get("/coin", (request, reply) => {
        coinCount({ denom: 5, count: 3 }, { denom: 10, count: 2 });
        coinCount(...coins);
        coinCount(coins);  
        reply  
        .code(200)
        .header("Content-Type", "text/html; charset=utf-8")

        .send(`<h2>Value of ${count} of ${denom} is ${coinValue}</h2><br /><a href="/">Home</a>`);
    });

    fastify.get("/coins", (request, reply) => {
      reply
        .code(200)
        .header("Content-Type", "text/html; charset=utf-8")

        .send(`<h2>Option ${option} value is ${coinValue}</h2><br /><a href="/">Home</a>`);
    });


    // Start server and listen to requests using Fastify
    const listenIP = "localhost";
    const listenPort = 8080;
    fastify.listen(listenPort, listenIP, (err, address) => {
      if (err) {
        console.log(err);
        process.exit(1);
      }
      console.log(`Server listening on ${address}`);
    });

    function validDenomination(coin) {
        const coinValues = [1, 5, 10, 25, 50, 100]
        if (coinValues.indexOf(coin) !== -1) {
            return true;
        }
        else {
            return false;
        }
    }

    function valueFromCoinObject(obj) {
        const denom = obj.denom;
        const count = obj.count;
        return (count * denom);
    }

    const valueFromArray = (arr) => {
        let total = arr.reduce((accumulator, current) => {
            return (accumulator += valueFromCoinObject(current));
        }, 0);
        return total;
    };

    export function coinCount(...coinage) {
        return valueFromArray(coinage);
    }

    const coins = [
        {denom: 25, count: 2},
        {denom: 1, count: 7}
    ];

    let coinObj = 
    {
      denom: 25,
      count: 3,
    };

    //console.log(validDenomination(2));
    //console.log(validDenomination(25));
    //console.log(valueFromCoinObject(coins[1]));
    //console.log(valueFromArray(coins));
    //console.log(coins[0]);
