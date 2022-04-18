# Ibc-community-pool
Using ibc contracts to manage community pool on foreign chain

## Motive
Each Cosmos Chain has a community pool which is a pool of tokens on the chain itself and is controlled by the gov module of that chain.

What if the gov module of that chain has controll over a pool of tokens but on another chain. In other words, what if a chain wants to have a community pool but on another chain. 

A `foreign community pool` can be really usefull. For example, takes juno on osmosis, juno community can use juno's `native community pool` to fund juno's `foreign community pool` on osmosis so that they can create external incentive gauges on any osmosis pools. Or it can be use to fund any utility contracts on osmosis that the juno community deems useful.

This repo implement that `foreign community pool` idea. The very requirement for this contract to work is both chain must have wasmd.

## How this thing works
So we have a pair of ibc contracts, one on osmosis (osmosis contract), the other on juno (juno contract).

Juno contract should be funded by the juno's `native community pool`. Once funded, it ibc-transfers all the fund to osmosis contract.

After that, `juno contract` ebstablish an ibc channel connecting to `osmosis contract`. This channel is for moving ibc packet from `juno contract` to `osmosis contract`

From now on, the juno community now has a `foreign community pool` on osmosis. If they want to do something with the foreign pool, they can use wasmd's `ExecuteContractProposal` to command the `juno contract` to send out abitrary `sdk.Msg` wrapped in ibc packet to `osmosis contract`. `Osmosis contract` will execute those `sdk.Msg` in the ibc packet.

![Alt text](Ibc-community1.png?raw=true "Title")






