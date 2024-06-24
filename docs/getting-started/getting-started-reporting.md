# Reporting

Reporting in Exchange can be broken down into three main sections. This includes Transactions, Virtual accounts, and Settlements. 

This makes up on how we report the daily funding cycle. 

<ul>
  <li> Transactions are loaded in every day, and reported at the transaction endpoint. These then load into the 'Trade Accounts', which are a subset of virtual accounts. 
  <li> Once the instructional funding window opens, the net amount moves into the Instructional Hold Account.
  <li> After instructions are sent, money will move into its respective virtual account.
  <li> Once the funding window closes, we will generate settlements for funding, and these will be reported on the settlement endpoint.
</ul>

<!-- type: row -->

<!-- type: card
title: See Transactions
description: Consume transaction loaded into Exchange 
link: ?path=docs/getting-started/getting-started-instfunding-net.md

-->
<!-- type: card
title: See Virtual Accounts
description: Review money movement through virtual accounts in the system
link: ?path=docs/getting-started/getting-started-instfunding-gross.md
-->

<!-- type: card
title: See Settlements
description: See settled amounts out to submerchants
link: ?path=docs/getting-started/getting-started-instfunding-split.md
-->
<!-- type: row-end -->
