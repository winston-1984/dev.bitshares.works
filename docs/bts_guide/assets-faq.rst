
.. _asset-faq:




Assets - FAQ
------------------

.. _asset-faq1:

Can I change `x` after creation of the asset
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The following parameters can be changed after creation:

* Issuer
* UIA-Options:

	* Max Supply
	* Market Fee
	* Permissions (disable only/nor re-enable)
	* Flags (if permissions allow it)
	* Core exchange rate
	* White/Black Listing
	* Description

* MPG-Options:

	* Feed Life Time
	* Minimum Feeds
	* Force Settlement Offset/Delay/Volume

Things that cannot be changes:

* Symbol
* Precision

A guide can be found :ref:`here <uia-update-manual>`.

.. _asset-faq2:

Can I change the issuer?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The current issue of an asset may transfer ownership of the asset to
someone else by changing the issuer in the asset's settings.

.. _asset-faq3:

What about Parent and Child assets?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

A **parent**/**child** relation ship for assets can be represented by
the name of the symbol, e.g.::

    PARENT.child

can only be created by the issuer of ``PARENT`` and no one else.

.. _asset-faq4:

What happens to the asset creation fee?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

50% of the asset creation fee are used to pre-fill the assets fee pool.
From the other 50%, 20% go to the network and 80% go to the referral
program. This means, that if you are a life-time member, you get back
40% of the asset creation fee after the vesting period (currently 90
days).

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
the fee pool and leave the issuer with his tokens at a slight loss
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
exchange rate updated unless he wants the owner of his asset to be
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

**Permissions** Give you the right to edit Flags 
**Flags** Allow you to enable or disable asset features

Once a permission to edit a flag is revoked, 
the flag setting under it is permanent; 
can never be modified again.

.. _asset-faq10:

What are the Flags?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``charge_taker_fee``:
  an issuer-specified percentage of all market trades in this asset is
  paid to the issuer.  Charged if the order is filled immediately.
  When the charge_maker_fee flag is selected, the user must enter a percent fee.
* ``charge_maker_fee``:
  like charge_taker_fee except charged when the order is **NOT** filled immediately. 
* ``white_list``:
  accounts must be white-listed in order to hold this asset
* ``override_authority``:
  issuer may transfer asset back to himself
* ``transfer_restricted``:
  require the issuer to be one party to every transfer
* ``disable_force_settle``:
  disable force settling
* ``global_settle``: (only for bitassets)
  allows bitasset issuer to force a global settling - this may be set
  in permissions, but should not be set as flag unless, for instance, a
  prediction market has to be resolved. If this flag has been enabled,
  no further shares can be borrowed!
* ``disable_confidential``:
  allow the asset to be used with confidential transactions
* ``witness_fed_asset``:
  allow the asset to be fed by witnesses
* ``committee_fed_asset``:
  allow the asset to be fed by the committee

 .. _asset-faq11:
 
What are the Permissions?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Enable maker fee
* Enable taker fee
* Require holders to be white-listed
* Issuer may transfer asset back to himself
* Issuer must approve all transfers
* Disable confidential transactions

.. _asset-faq12:

What happens if I enable Maker and Taker Market fees?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Market fees allow an asset issuer to charge a variable transaction fee 
based on the size of the transaction.

A "Maker" is one who adds an order onto the orderbooks by making an offer
A "Taker" is one who removes an order from the orderbooks by filling it

If *Maker and Taker Market Fees* Flags of a UIA are turned on, 
fees have to be payed for each **market transaction**. 
This means, that market fees only apply to **filled orders**!

The percentage of market fees that are applied can be defined and
changed by the issuer.  The issuer may charge a diferent fee depending on 
if the user is a Maker or Taker.

If the Maker Fee is set to 0.1%, the issuer will earn 0.1% of market volume
as profit when the trader leaves an order on the orderbooks. 

If the Taker Fee is set to 0.2%, the issuer will earn 0.2% of market volume
as profit when the trader takes an order off the orderbooks. 

For a simple Market Fee, an asset issuer may set Maker and Taker fees to match; 
charging both parties equally.  By exposing both fees seperately, an asset 
issuer can choose to require a larger Taker than Maker fee to encourage 
populating the orderbook with liquidity.  

Prior to BSIP81 there was only one Market Fee.  At the transition both Maker 
and Taker fees for all existing assets were set to the previous Market Fee.

The profits accumulated by market fess for each UIA and can be withdrawn 
by the issuer.

.. _asset-faq13:

How are market fees accounted in a trade?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In BitShares, you pay the fee upon **receiving an asset**, suppose:

bob, owner of bob_UIA sets:

    Maker fee for bob_UIA market at 0.1%
    Taker fee for bob_UIA market at 0.2%
    
alice, owner of alice_UIA set:

    Maker fee for alice_UIA market at 0.3%
    Taker fee for alice_UIA market at 0.4%

charlie places a limit order to buy bob_UIA with alice_UIA onto the order book.
daniel, fills charlie's order by selling bob_UIA to receive alice_UIA.

charlie is a `bob_UIA:alice_UIA` market **Maker**
    charlie *recieves* `bob_UIA`
	charlie pays bob 0.1%

daniel is a **Taker** in the `bob_UIA:alice_UIA` market
    daniel *receives* `alice_UIA`
	daniel pays alice 0.4% 




---------  
   
  
Market Pegged Assets
------------------------

.. _asset-faq14:

Can I use the same flags/permissions as for UIAs?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Yes!

.. _asset-faq15:

What are market-pegged-asset-specific parameters?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* ``feed_lifetime_sec``:
  The lifetime of a feed. After this time (in seconds) a feed is no
  longer considered *valid*.
* ``minimum_feeds``:
  The number of feeds required for a market to become (and stay) active.
* ``force_settlement_delay_sec``:
  The delay between requesting a settlement and actual execution of
  settlement (in seconds)
* ``force_settlement_offset_percent``:
  A percentage offset from the price feed for settlement (`100% = 10000`)
* ``maximum_force_settlement_volume``:
  Maximum percentage of the supply that can be settled per day (`100% = 10000`)
* ``short_backing_asset``:
  The asset that has to be used to *back* this asset (when borrowing)

  
---------------------

|  
