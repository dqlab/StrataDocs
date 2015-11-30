---
title: Products - Swaption
permalink: /swaption/
---

## Swaption 

A swaption is a financial instrument that provides an option based on the future value of an interest rate swap.
The option is European, exercised only on the exercise date.

For example, a swaption might involve an option which expires in 2Y years on an agreement to exchange the difference between the fixed rate of 1% and the 'GBP-LIBOR-3M' rate every 3 months for 5 years.


## Key classes

A swaption is represented in Strata using the [`Swaption`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/fra/Fra.html) class.
The `Swaption` class stores details of the product that was agreed.
The trade details are stored in [`SwaptionTrade`]({{site.baseurl}}/apidocs/com/opengamma/strata/product/swaption/SwaptionTrade.html) class.

A `Swaption` can be created using a builder as follows:

```java
Swaption swaption = Swaption.builder()
        .expiryDate(AdjustableDate.of(LocalDate.of(2014, 6, 14), ADJUSTMENT))
        .expiryTime(LocalTime.of(10, 0))
        .expiryZone(ZoneId.of("Z"))
        .longShort(LongShort.LONG)
        .swaptionSettlement(PhysicalSettlement.DEFAULT)
        .underlying(SWAP)
        .build();
```

where the expiry date is specified in terms of `AdjustableDate` with a suitable `BusinessDayAdjustment`, and `SWAP` represents the underlying swap product. 

The swaption settlement type is `PhysicalSettlement` or `CashSettlement`, and further detail of cash settled swaptions is defined by `CashSettlementMethod`.  These correspond to the ISDA 2006 definitions.


## Pricing

The `strata-pricer` module provides pricing support for swaptions based on lognormal (Black) model, normal (Bachelier) model and SABR model.

For physical-delivery swaptions, the pricer classes are

* [`BlackSwaptionPhysicalProductPricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/BlackSwaptionPhysicalProductPricer.html) class.
* [`NormalSwaptionPhysicalProductPricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/NormalSwaptionPhysicalProductPricer.html) class.
* [`SabrSwaptionPhysicalProductPricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/SabrSwaptionPhysicalProductPricer.html) class.
* [`BlackSwaptionPhysicalTradePricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/BlackSwaptionPhysicalTradePricer.html) class.
* [`NormalSwaptionPhysicalTradePricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/NormalSwaptionPhysicalTradePricer.html) class.
* [`SabrSwaptionPhysicalTradePricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/SabrSwaptionPhysicalTradePricer.html) class.

For cash-settled swaptions, the pricer classes are

* [`BlackSwaptionCashParYieldProductPricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/BlackSwaptionCashParYieldProductPricer.html) class.
* [`NormalSwaptionCashParYieldProductPricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/NormalSwaptionCashParYieldProductPricer.html) class.
* [`SabrSwaptionCashParYieldProductPricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/SabrSwaptionCashParYieldProductPricer.html) class.
* [`BlackSwaptionCashParYieldTradePricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/BlackSwaptionCashParYieldTradePricer.html) class.
* [`NormalSwaptionCashParYieldTradePricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/NormalSwaptionCashParYieldTradePricer.html) class.
* [`SabrSwaptionCashParYieldTradePricer`]({{site.baseurl}}/apidocs/com/opengamma/strata/pricer/swaption/SabrSwaptionCashParYieldTradePricer.html) class.

The following pricing methods are available in common:

* present value
* present value sensitivity
* currency exposure
* current cash
* implied volatility

For Black and Normal methods, the Greeks are computed:

* present value delta
* present value gamma
* present value theta
* present value sensitivity to volatility, i.e., present value vega

SABR model pricer instead supports

* SABR parameter sensitivity


## Product model

The following table summarizes the fields on `Swaption` that can be used to control the product.
For more detail on the meaning of each field, see the [Javadoc]({{site.baseurl}}/apidocs/com/opengamma/strata/product/Swaption/Swaption.html);

| Property name     | Description | Optional   |
|-------------------|-------------|------------|
| longShort         | Whether the swaption is long or short | Required |
| swaptionSettlement| The settlement method | Required |
| expiryDate        | The expiry date | Required |
| expiryTime        | The expiry time | Required |
| expiryZone        | The time-zone of the expiry time | Required |
| underlying        | The underlying swap | Required |



