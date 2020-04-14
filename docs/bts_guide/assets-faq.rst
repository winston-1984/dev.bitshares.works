
.. _asset-faq:




Assets - FAQ
------------------

.. _asset-faq1:

Can I change `x` after creation of the asset?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following parameters can be changed after creation:

* Issuer
     
      At core level, there is one `issuer` for each UIA or MPA, which controls access 
      to the asset permissions. As the MPA `issuer` cannot actually issue shares, they are
      referred to in this document as the MPA Admin.

* User Issued Asset (UIA) Options:

    * Max Supply
    * Market Fee
    * Permissions (disable only/nor re-enable)
    * Flags (if permissions allow it)
    * Core exchange rate
    * White/Black Listing
    * Description

* Market Pegged Asset (MPA) Options:

    * Feed Life Time
    * Minimum Feeds
    * Force Settlement Offset/Delay/Volume/Disable
    * Short Backing Asset 
    * Retain Power to Force Global Settlement
    * Margin Call Fee Ratio
    * Whitelist feed producer Oracles
    * Whitelist Committee and Witnesses as Oracles
    
* MPA Feed Producers Options:

    * Price Feed
    * Core Exchange Rate (CER)
    * Maximum Short Squeeze Ratio (MSSR)
    * Maintenance Collateral Ratio (MCR)
        
* These settings that **cannot** be changed after asset creation:

    * Symbol
    * Precision
    * (MPA) Short Backing Asset 




What actors are relevent to Assets?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
The Graphene Asset `issuer` Actor:

At the core level, there is only one `issuer` and it is the creator and current principal of a UIA or MPA. 

When we speak about the `issuer` it is more comfortable to speak in terms of what powers the issuer weilds:

    Asset Creator

      At the time of Asset creation, certain duties are given to the Creator such as 
      assigning the maximum coins in supply.  This applies to both UIA and MPA Assets.

    Asset Principal

      After the Asset creation, there are various settings under control of 
      the Asset Principal. Additionally, the asset principal collects all asset fees.  
      Also, assigning the Principal to another user transfers all other `issuer` rights.  
      Principals can be dividided in two categories; UIA Issuers and MPA admins. 

        UIA Issuer

          A UIA Principal is called the UIA Issuer, because he has the authority 
          to issue UIA's to UIA Holders.   

            UIA Gateway 
             
              Some UIA Issuers offer 1:1 backing of a UIA for a coins on another blockchain 
              such as Bitcoin, fiat currency, or other money, these issuers are UIA Gateways.

        MPA Admin

          MPA's cannot be issued to Holders by the Principal.  Therefore, the Principal of an 
          MPA is an "Administrator" who assigns and incentivizes the Price Feed publisher Oracles.  
          The MPA Admin also has control over the same UIA settings as a UIA Issuer, as well 
          as additional MPA specific settings. 

            

Other non-issuer Actors:

    UIA Holder

      A UIA holder has either purchased the UIA from another Holder or has been 
      issued the Asset by the UIA Issuer.  The Holder has UIA transfer rights.
      If the UIA was issued by a Gateway, the Holder may have Gateway priviledges 
      to swap UIA's for off chain cold storage assets, subject to availability. 

    MPA Borrower

      The MPA Borrower is in effect the MPA Issuer and assumes transfer rights upon issuance.
      The Borrower enters a call position to issue an MPA to himself, in exchange for signing 
      a smart contract, which he backs by locking collateral under the required call order terms.
      The Borrower's collateral value is subject to the price published by Oracles.  Failure 
      to maintain adequate collateral amount, results in forfeiture of the Borrower's collateral
      under margin call.  The Borrower is also subject to Force Settlment by MPA Holders and Global 
      Settlement both directly by the MPA Admin and the call contract terms.

    MPA Holder

      The Holder has purchased the MPA from a Borrower or another Holder.  Like the Borrower,
      the Holder has MPA transfer rights.  Additionally, the Holder has MPA settlement rights. 

    MPA Oracle

      The Oracle is the Price Feed publisher for the MPA smart contract's terms.   The MPA Admin
      may assign mulitple Oracles and the blockchain considers the median of their Price Feeds 
      when evaluating call contracts.  It is the Oracle's job to collect real world 
      prices and publish them to the blockchain periodically.


A guide can be found :ref:`here <uia-update-manual>`.
There is also more information about each option in the FAQ's below:

.. _asset-faq2:

How do I transfer ownership to a new Issuer?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The current Asset Principal of an asset may transfer control of the asset to
someone else by changing the `issuer` in the asset's settings.  

.. _asset-faq3:

What about Parent and Child assets?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A **parent**/**child** relationship for assets can be represented by
the name of the symbol, e.g.:

    PARENT.child

The parent asset controller owns the child namespace and can create any 
PARENT.xxx.  Such child assets can only be created by the controller of 
``PARENT``. Both PARENT and child assets can be both MPA's or UIA's. 

.. _asset-faq4:

What happens to the asset creation fee?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

50% of the asset creation fees are used to pre-fill the assets fee pool.
From the other 50%, 20% go to the network and 80% go to the referral
program. This means, that if you are a life-time member, you get back
40% of the asset creation fee after the vesting period (currently 90
days).  An additional 40% would be in the fee pool owned and to be claimed
at will by the creator. 

---------

Fee Pool
------------

.. _asset-faq5:

What is Fee Pool Draining?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If an order is created and paid in a non-BTS asset, the fee is
implicitly exchange into BTS to pay the network fee. However, if the
order is canceled, 90% of the fee will be returned as BTS. The result
is, that if the core exchange rate is lower than the highest bid, people
can simply buy your token from the market, and exchange them implicitly
with the fee pool by creating and canceling an order. This will deplete
the fee pool and leave the Issuer with his tokens at a slight loss
(depending on the offset of the core exchange rate). For this reason, we
recommend to use a core exchange that is slightly higher than the market
price of your asset. As a consequence, paying fees in BTS should always
be cheaper.

.. _asset-faq6:

What is the fee pool all about?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The fee pool allows participants in the network to deal with assets and
pay for the transaction fees without the need to hold BTS. Any
transaction fee can be paid by paying any asset that has a core exchange
rate (i.e. a price) at which the asset can be exchange implicitly into
BTS to cover the network fee. If the asset's fee pool is funded, the
fees can be payed in the native UIA instead of BTS.

.. note:: The core exchange rate at which a fee can be exchanged into
          BTS may differ from the actual market valuation of the asset.
          A user, thus, may pay a premium or spare funds by paying in
          BTS.

.. warning:: Make sure your core exchange rate is higher than the lowest
             ask, otherwise, people will buy your token from the market
             and drain your fee pool via implicit abitrage.

It is the task of the issuer to keep the fee pool funded and the core
exchange rate updated unless he wants the holder of his asset to be
required to hold BTS for the fee.

.. _asset-faq7:

What to do if the fee pool is empty?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Open up the issuer's account, click the assets tab and open up the
dialog to change the asset. There will be a fee pool tab that allows you
to fund the fee pool and claim the accumulated fees!


---------

Market Fees
---------------

.. _asset-faq9:

What are Asset Flags and Permissions?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

When an asset is created, the issuer can set any combination of
flags/permissions. 

**Permissions** give you the right to edit Flags 

**Flags** allow you to enable or disable asset features

Permissions are permanent one way switches.  Once a Permission to 
edit a Flag is renounced by the issuer, the Flag setting(s) 
under it remain but but can never be modified again.  As such, 
Permissions should be given due consideration prior to disabling.

.. _asset-faq10:

What are the Flags?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* `charge_market_fee`
  an issuer-specified percentage of all market trades in this asset is
  paid to the issuer.  When set, charge_market_fee allows the issuer to
  charge a Taker fee if an order is filled immediately, or a Maker fee 
  when the order is **NOT** filled immediately.  
* `white_list`
  accounts must be white-listed in order to hold this asset
* `override_authority`
  issuer may transfer asset back to himself
* `transfer_restricted`
  require the issuer to be one party to every transfer
* `disable_force_settle`
  disable force settling
* `disable_confidential`
  allow the asset to be used with confidential transactions  
  
 .. _asset-faq11:
 
What are the Permissions?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Enable market fee
* Require holders to be white-listed
* Issuer may transfer asset back to himself
* Issuer must approve all transfers
* Disable confidential transactions

.. _asset-faq12:

What happens if I enable Market fees?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Market fees allow an asset issuer to charge a variable transaction fee 
based on the size of the transaction.  

If *Market Fees* Flag of a UIA is turned on, 
fees have to be payed for each **market transaction**. 
This means, that market fees only apply to **filled orders**!

The percentage of market fees that are applied can be defined and
changed by the issuer.  The issuer may charge a different fee depending on 
if the user is a Maker or Taker.

What is a Maker and a Taker?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A "Maker" adds a limit order onto the orderbooks by making an offer

A "Taker" is one who removes a Maker's order from the orderbooks by filling it

If the Maker Fee is set to 0.1%, the issuer will earn 0.1% of market volume
as profit when the Maker leaves an order on the orderbooks, if that order
is later filled by a Taker. 

If the Taker Fee is set to 0.2%, the issuer will earn 0.2% of market volume
as profit when the Taker takes a Maker's order off the orderbooks. 

For a simple Market Fee, an asset issuer may set Maker and Taker fees to match; 
charging both parties equally.  By treating the fees seperately, an asset 
issuer can choose to require a larger Taker than Maker fee to incentivize
populating the orderbook with liquidity.  

Prior to BSIP81 there was only one Market Fee.  At the transition both Maker 
and Taker fees for all existing assets were set to the previous Market Fee.
In core at BSIP81, the maker fee object keeps the lineage of the market fee and 
the taker fee is a new object which shows zero fee on each transaction
until after the hard fork.  

The profits accumulated by market fess for each UIA and can be withdrawn 
by the issuer.

NOTE: Graphene precision for percentage is in hundredths of a percent;
100% is expressed as ten thousand (10000). the Reference UI includes the 
translation to traditional percent format. 

.. _asset-faq13:

What happens when assets have different fees?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In BitShares, you pay a fee upon **receiving an asset**.

**Scenario:**

bob, Issuer of `bob_UIA` sets:

    * Maker fee for `bob_UIA` market at 0.1%
    
    * Taker fee for `bob_UIA` market at 0.2%
    
alice, Issuer of `alice_UIA` sets:

    * Maker fee for `alice_UIA` market at 0.3%
    
    * Taker fee for `alice_UIA` market at 0.4%

charlie places a limit order to buy `bob_UIA` with `alice_UIA` onto the book.

daniel, fills charlie's order by selling `bob_UIA` to `receive alice_UIA`.

**charlie and bob's outcome:**

  * charlie is a `bob_UIA:alice_UIA` market Maker
  
  * charlie receives `bob_UIA`
  
    * charlie pays bob 0.1% Maker Fee
    
**daniel and alice's outcome:**

  * daniel is a Taker in the `bob_UIA:alice_UIA` market
  
  * daniel receives `alice_UIA`
  
    * daniel pays alice 0.4% Taker Fee

**daniel owes no fee to bob and charlie owes no fee to alice**

Sharing Market Fees with the Committee
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

After Hard Fork BSIP86 a percent of UIA Issuer's and MPA Admins's Market Fees is itself
subject to a fee by the BitShares Committee.  These funds go to the committee 
controlled account's vesting balances. At HF BSIP86 the maximum 
`market_fee_network_percent` (MFNP) was hard coded to 30% of the market fee. 
The default MFNP fee was set to zero. The committee holds the right to adjust 
the MFNP in range from 0 to 30, as they deem fit, to fund development.  The 
MFNP applies to all UIA's and MPA's Market Fees equally. 
 
   
Market Pegged Assets
------------------------

.. _asset-faq14:

Can I use the same flags/permissions as for UIAs?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Yes! However, MPA's introduce many additional Admin options. 

.. _asset-faq15:

What are market-pegged-asset-specific parameters?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

MPA specific parameters are per-asset parameters, which include:

* ``feed_lifetime_sec``:
    The lifetime of a feed.  After this time (in seconds) a feed is no
    longer considered *valid*.  The final feed price is the median 
    of all valid feeds submitted by the price feed producer oracles.
* ``minimum_feeds``:
    The number of feeds required for a market to become (and stay) active.
* ``force settling``:
    * ``disable``:
        An MPA Admin may choose to disallow an asset holder from having the power 
        to compel an MPA Borrower to settle a margin position at feed price.
    * ``delay seconds``:
        The delay between requesting a settlement and actual execution of
        settlement (in seconds).
    * ``maximum volume``:   `100% = 10000 graphene`
        Maximum percentage of the asset supply that can be settled daily 
    * ``Force Settlment Offset (FSO)``:   `100% = 10000 graphene`
        Percentage offset from the price feed for settlement favoring the borrower. 
    * ``Force Settlement Fee Percentage (FSFP)``:
   
        FSFP is set by the MPA Admin and provides a revenue stream for 
        the Admin.  When a force-settlement order is executed by 
        an Asset Holder, he sells:  
            
            `MPA quantity X`
        
        and in return receives (executes right to buy) collateral in the amount:
        
           `X * (1 - FSO) * (1 - FSFP) / feed_price` 
         
        The settled debt position's borrower is complelled to buy:
         
            `MPA quantity X`
         
        The the borrower is compelled to provide (sell) collateral in quantity: 
         
           `X * (1 - FSO) / feed_price` 
         
        The delta between paid and received collateral in quantity: 
         
           `X * FSFP * (1 - FSO) / feed_price` 
         
        is paid to the MPA Admin as Force Settlement Fee.

--------- 
* ``allow MPA Admin to force global settlement``: 
    This permission effectively allows the issuer to margin call every 
    borrower.  Even if this Permission is renounced, the same power can be had
    through publishing a high maintenance collateral ratio or erroneous price.  
    If this flag has been enabled, no further shares can be borrowed!
* ``short backing asset``: 
    The asset that must be used as collateral to *back* this asset (when borrowing).
    NOTE: This setting can only be established once when creating the asset.
* ``margin call fee ratio(MCFR)``: 
    The MPA Admin may declare a MCFR to collect a fee from margin calls of his asset. 
    Margin call order price limit is: `settlement_price / ( MSSR - MCFR )`
    Upon settlement of a margin call, the issuer collects: 
    `( amount_settled * MCFR ) / settlement_price` 
* ``whitelist feed producers``: 
    The MPA Admin must manually whitelist feed producers in a list by user_id.
    These feed producers are the oracles which gather data and upload it to the blockchain.
    The feed producer's median price is used in all MPA smartcoin margin contracts.
* ``allow witness or committee to feed``: (per-asset parameter)
    In addition to manually whitelisted producers the MPA Admin may choose to 
    allow all witnesses or all committe members, each as a group, to be feed producers.   
* ``Feed Producers``: 
    Feed producers are chosen by the MPA Admin in list format by 1.2.x user_id.  
    The feed producer publishes 4 rates to the blockchain for each MPA (price and 3 
    coefficients: CER, MSSR, and MCR), the element wise median of these price feeds 
    is the oracle which enforces the outcome of margin loans: 
    
    * ``price feed (FEED)``:
        Each feed producer, assigned by the MPA Admin, may publish a price feed.  The 
        feed represents the price of the MPA, relative to its short backing asset.  Each
        feed producer is tasked with gathering real world market data, normalizing it, 
        in some instances applying a cross rate, and then regularly uploading it to 
        the blockchain. 
    * ``core exchange rate (CER)``:
        Fees are by default paid in BTS. However, the user may opt to pay their fee in 
        smartcoin terms. When paying these fees in terms other than BTS the user is 
        subject to a fee of:  `CER * FEED * BTS_DUE`.
    * ``maximum short squeeze ratio (MSSR)``:
        When a call order is liquidated, it is subject to be discounted at `1 / MSSR` 
        below the settlement price, when placed on the order book. 
    * ``Maintenance Collateral Ratio (MCR)``:
        When you take a loan, the blockchain periodically tests that you have enough
        collateral, given the current:  `MCR * FEED * YOUR_DEBT`.
   

---------------------

|  
