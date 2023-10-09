Usage
=====

.. _installation:

Installation
------------

To use cvehunter, first install it using pip:

.. code-block:: console

   pip3 install cvehunter

Basic example
----------------

.. code-block:: python

   import asyncio
   from cvehunter import CveHunter
   
   async def test() -> None:
       ch = CveHunter()
       
       cve = await ch.search_by_cve("CVE-2023-41991")
       
       print(cve.cve_id)
       "CVE-2023-41991"

       print(cve.cwe_id)
       "CWE-295"

       print(cve.description)
       "A certificate validation issue was addressed. This issue is fixed in macOS Ventura 13.6, iOS 16.7 and iPadOS 16.7. A malicious app may be able to bypass signature validation. Apple is aware of a report that this issue"

       print(cve.cvss_v3)
       {'score': 5.5, 'vector': 'CVSS:3.1/AV:L/AC:L/PR:N/UI:R/S:U/C:N/I:H/A:N', 'severity': 'MEDIUM', 'version': 3.1, 'exploitability': 1.8, 'impact': 3.6}
       
   asyncio.run(test())

