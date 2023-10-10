Usage
=====

.. _installation:

Installation
------------

To use cvehunter, first install it using pip:

.. code-block:: console

   pip3 install cvehunter

Initialization
---------------

To create a `CveHunter` instance, you can specify an optional proxy dictionary. This proxy can be used to make HTTP requests through a proxy server.

.. code-block:: python

   from cvehunter import CveHunter

   # Initialize without a proxy
   hunter = CveHunter()

   # Initialize with a proxy (replace with your actual proxy settings)
   proxy_settings = {
       "http": "http://proxy.example.com:8080",
       "https": "https://proxy.example.com:8080"
   }
   hunter_with_proxy = CveHunter(proxy=proxy_settings)

Checking Connection
-------------------

You can use the `check_connection` method to verify if the `CveHunter` can connect to the NVD (National Vulnerability Database) API.

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

   # Parameters:
   # - cve_id (str, required): The CVE ID to search for data.

Searching by CPE ID
-------------------

You can use the `search_by_cpe` method to search for CVEs based on a CPE (Common Platform Enumeration) ID.

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

   # Parameters:
   # - cpe_id (str, required): The CPE ID to search for CVEs.
   # - limit (int, optional): Maximum number of results to return. Default is None (no limit).
   # - only_vulnerable (bool, optional): Limit results to only include the vulnerable ones. Default is None.
   # - start_date (str, optional): Start date for filtering CVEs based on publication date. Default is None.
   # - end_date (str, optional): End date for filtering CVEs based on publication date. Default is None.

Searching by CVSS Vector
------------------------

You can use the `search_by_vector` method to search for CVEs based on a CVSS (Common Vulnerability Scoring System) vector and version.

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

   # Parameters:
   # - cvss_version (int, required): The CVSS version (2 or 3) to use for the search.
   # - vector (str, required): The CVSS vector representing the vulnerabilities.
   # - limit (int, optional): Maximum number of results to return. Default is None (no limit).
   # - start_date (str, optional): Start date for filtering CVEs based on publication date. Default is None.
   # - end_date (str, optional): End date for filtering CVEs based on publication date. Default is None.

Searching by CWE ID
-------------------

You can use the `search_by_cwe` method to search for CVEs based on a CWE (Common Weakness Enumeration) ID.

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

   # Parameters:
   # - cwe_id (str, required): The CWE ID to search for CVEs.
   # - limit (int, optional): Maximum number of results to return. Default is None (no limit).
   # - start_date (str, optional): Start date for filtering CVEs based on publication date. Default is None.
   # - end_date (str, optional): End date for filtering CVEs based on publication date. Default is None.
