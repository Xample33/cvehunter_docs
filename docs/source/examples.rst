CveHunter Example Usage
=======================

This guide provides a variety of usage examples for the `CveHunter` class, along with explanations of the variables returned by each function.

Initialization
---------------

To begin, you need to initialize the `CveHunter` class. You can do this with or without a proxy dictionary. Here's how you can initialize it:

.. code-block:: python

   from cvehunter import CveHunter

   # Initialize CveHunter without a proxy
   hunter = CveHunter()

   # Initialize CveHunter with a proxy (replace with your actual proxy settings)
   proxy_settings = {
       "http": "http://proxy.example.com:8080",
       "https": "https://proxy.example.com:8080"
   }
   hunter_with_proxy = CveHunter(proxy=proxy_settings)

Checking Connection
-------------------

You can use the `check_connection` method to check if the connection to the NVD (National Vulnerability Database) API is working. This method returns a boolean value (`True` if the connection is successful, `False` otherwise).

.. code-block:: python

   from cvehunter import CveHunter

   # Initialize CveHunter
   hunter = CveHunter()

   # Check the connection to NVD API
   is_connected = await hunter.check_connection()

   if is_connected:
       print("Connection to NVD API successful")
   else:
       print("Connection to NVD API failed")

Searching by CVE ID
-------------------

You can use the `search_by_cve` method to retrieve information about a specific CVE by its CVE ID. This method returns a `Cve` object containing the following variables:

- `cve_id` (str): The CVE ID.
- `description` (str): A description of the CVE.
- `source` (str): The source identifier.
- `cwe_id` (str or None): The CWE ID (Common Weakness Enumeration) associated with the CVE, or `None` if not available.
- `references` (list of str): A list of URLs referencing the CVE.
- `cvss_v2` (Cvss or None): An optional `Cvss` object representing CVSS version 2 details, or `None` if not available.
- `cvss_v3` (Cvss or None): An optional `Cvss` object representing CVSS version 3 details, or `None` if not available.
- `published_date` (str): The publication date of the CVE.
- `updated_date` (str): The last modified date of the CVE.

.. code-block:: python

   from cvehunter import CveHunter

   # Initialize CveHunter
   hunter = CveHunter()

   # Search for information about a CVE by its CVE ID
   cve_id = "CVE-2023-41991"
   cve_info = await hunter.search_by_cve(cve_id)

   if cve_info:
       print(f"CVE ID: {cve_info.cve_id}")
       print(f"Description: {cve_info.description}")
       print(f"Source: {cve_info.source}")
       print(f"CWE ID: {cve_info.cwe_id}")
       print(f"References: {', '.join(cve_info.references)}")
       print(f"Published Date: {cve_info.published_date}")
       print(f"Updated Date: {cve_info.updated_date}")

Searching by CPE ID
-------------------

You can use the `search_by_cpe` method to search for CVEs based on a CPE (Common Platform Enumeration) ID. This method returns a list of CVE IDs that match the search criteria.

.. code-block:: python

   from cvehunter import CveHunter

   # Initialize CveHunter
   hunter = CveHunter()

   # Search for CVEs based on a CPE ID
   cpe_id = "cpe:2.3:o:microsoft:windows_10:1607:*:*:*:*:*:*:*"
   cve_ids = await hunter.search_by_cpe(cpe_id, limit=10, only_vulnerable=True, start_date="2023-01-01", end_date="2023-12-31")

   if cve_ids:
       print(f"CVE IDs matching the CPE ID {cpe_id}:")
       for cve_id in cve_ids:
           print(cve_id)

Searching by CVSS Vector
------------------------

You can use the `search_by_vector` method to search for CVEs based on a CVSS (Common Vulnerability Scoring System) vector and version. This method returns a list of CVE IDs that match the search criteria.

.. code-block:: python

   from cvehunter import CveHunter

   # Initialize CveHunter
   hunter = CveHunter()

   # Search for CVEs based on a CVSS vector and version
   cvss_version = 3
   cvss_vector = "AV:N/AC:H/PR:N/UI:N/S:U/C:H/I:H/A:H"
   cve_ids = await hunter.search_by_vector(cvss_version, cvss_vector, limit=5, start_date="2023-01-01", end_date="2023-12-31")

   if cve_ids:
       print(f"CVE IDs matching the CVSS vector {cvss_vector} (CVSS version {cvss_version}):")
       for cve_id in cve_ids:
           print(cve_id)

Searching by CWE ID
-------------------

You can use the `search_by_cwe` method to search for CVEs based on a CWE (Common Weakness Enumeration) ID. This method returns a list of CVE IDs that match the search criteria.

.. code-block:: python

   from cvehunter import CveHunter

   # Initialize CveHunter
   hunter = CveHunter()

   # Search for CVEs based on a CWE ID
   cwe_id = "CWE-78"
   cve_ids = await hunter.search_by_cwe(cwe_id, limit=10, start_date="2023-01-01", end_date="2023-12-31")

   if cve_ids:
       print(f"CVE IDs matching the CWE ID {cwe_id}:")
       for cve_id in cve_ids:
           print(cve_id)

