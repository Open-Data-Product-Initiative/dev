# Hello world example

> Example of complete working Data Product specification instance:

```yml

---
schema: 'https://opendataproducts.org/v3.1/schema/odps.yaml'
version: 4.0
product:
  contract:
    id: 02323M123
    type: ODCS
    contractVersion: 2.2.2
    contractURL: 'https://datamesh-manager.com/urbanltd/dataproducts/9bd530'
  details:
    en:
      name: UrbanPulse Events
      productID: urbanpulse-events-001
      valueProposition: >-
        Enable smarter city experiences by providing structured, real-time
        public event data ready for integration into travel apps, tourism
        platforms, and smart city services.
      description: >-
        UrbanPulse Events is a SmartCity data product that aggregates and
        structures public event information — concerts, exhibitions, festivals,
        sports events — making it accessible through APIs and dashboards for
        internal and future external use.
      productSeries: SmartCity Living Data Products
      visibility: internal
      status: production
      productVersion: 0.1.0
      versionNotes: >-
        Initial internal release with basic event metadata structure and shadow
        pricing model implemented.
      issues: >-
        Current limitations include manual ingestion of some event sources and
        partial metadata for smaller events. These will be addressed in the next
        update with automated feeds and metadata enrichment.
      categories:
        - city-events
        - tourism
        - smartcity
      standards:
        - ODPS 4.0
      tags:
        - smartcity
        - events
        - tourism
        - public-data
      brandSlogan: Turning City Buzz into Business Value
      type: dataset
  pricingPlans:
    declarative:
      en:
        - name: Basic Reader
          priceCurrency: USD
          price: 0
          billingDuration: month
          unit: recurring
          maxTransactionQuantity: 100
          offering:
            - Standard access to event metadata
            - Up to 100 SQL queries per month
            - Shared SLA (best-effort availability)
            - No prioritization in case of peaks
          notes: >-
            Shadow pricing only for internal visibility. No actual billing
            applied.
          paymentGateway:
            $ref: '#/product/paymentGateways/default'
          dataQuality:
            $ref: '#/product/dataQuality/default'
          SLA:
            $ref: '#/product/SLA/default'
          access:
            $ref: '#/product/dataAccess/API'
        - name: Extended User
          priceCurrency: USD
          price: 300
          billingDuration: month
          unit: recurring
          maxTransactionQuantity: 1000
          offering:
            - Prioritized SQL access during high-demand periods
            - Up to 1000 SQL queries per month
            - Faster response times
            - Moderate rate limits
          notes: >-
            Shadow pricing estimate based on infrastructure and operational cost
            models.
          paymentGateway:
            $ref: '#/product/paymentGateways/default'
          dataQuality:
            $ref: '#/product/dataQuality/default'
          SLA:
            $ref: '#/product/SLA/default'
          access:
            $ref: '#/product/dataAccess/API'
        - name: High Volume Access
          priceCurrency: USD
          price: 2000
          billingDuration: month
          unit: recurring
          maxTransactionQuantity: 500000
          offering:
            - Dedicated API channel for bulk usage
            - 'Up to 500,000 SQL queries per month'
            - Guaranteed SLA for availability and response time
          notes: Shadow pricing for strategic high-usage internal consumers.
          paymentGateway:
            $ref: '#/product/paymentGateways/agent'
          dataQuality:
            $ref: '#/product/dataQuality/premium'
          SLA:
            $ref: '#/product/SLA/premium'
          access:
            $ref: '#/product/dataAccess/Agent'
  SLA:
    declarative:
      default:
        name:
          en: The Basic SLA
        description:
          en: The basic SLA package
        dimensions:
          - dimension: uptime
            displaytitle:
              en: Uptime
            objective: 90
            unit: percent
          - dimension: responseTime
            objective: 200
            unit: milliseconds
          - dimension: updateFrequency
            objective: 30
            unit: minutes
      premium:
        name:
          en: The Premium SLA
        description:
          en: The Premium SLA package
        dimensions:
          - dimension: uptime
            displaytitle:
              en: Uptime
            objective: 99
            unit: percent
          - dimension: responseTime
            objective: 100
            unit: milliseconds
          - dimension: updateFrequency
            objective: 5
            unit: minutes
    support:
    phoneNumber: '+971508976456'
    phoneServiceHours: Mon–Fri 8am–4pm (GMT)
    email: support@opendataproducts.org
    emailServiceHours: Mon–Fri 8am–4pm (GMT)
    documentationURL: ''

  dataQuality:
    declarative:
      default:
        displaytitle:
          en: The Basic Data Quality
        description:
          en: The basic quality package
        dimensions:
          - dimension: accuracy
            displaytitle:
              en: Data Accuracy (percent)
            description:
              en: >
                Data Accuracy ensures the data product reflects the real-world
                entities or events it represents, minimizing errors and providing
                reliable insights.
            objective: 90
            unit: percentage
          - dimension: completeness
            displaytitle:
              en: Data Completeness (percent)
            objective: 90
            unit: percentage
      premium:
        displaytitle:
          en: The Premium Data Quality
        description:
          en: The premium quality package
        dimensions:
          - dimension: accuracy
            displaytitle:
              en: Data Accuracy (percent)
            description:
              en: >
                Data Accuracy ensures the data product reflects the real-world
                entities or events it represents, minimizing errors and providing
                reliable insights.
            objective: 98
            unit: percentage
          - dimension: completeness
            displaytitle:
              en: Data Completeness (percent)
            objective: 99
            unit: percentage
  dataAccess:
    default:
      name:
        en: Access to zipped package
      description:
        en: Latest Dataset and Resources
      outputPorttype: file
      format: zip
      accessURL: url to file as zip
    dataonly:
      name:
        en: Access to latest dataset
      description:
        en: Latest Dataset
      outputPorttype: file
      format: CSV
      accessURL: url to file as CSV
    API:
      outputPorttype: API
      authenticationMethod: OAuth
      specification: OAS
      format: JSON
      accessURL: 'https://data.cms.gov/data-api/v1/dataset/2/data'
      specsURL: 'https://data.cms.gov/provr-enrollment/api-docs'
      documentationURL: 'https://data.cms.gov/provr-enrollment/docs'
    Agent:
      outputPorttype: AI
      description:
        en: MCP interface for structured data access and agent interaction.
      authenticationMethod: Token
      specification: MCP 2025-03-26
      format: MCP
      specsURL: 'https://urbanpulse.ai/llms.txt'
      documentationURL: 'https://urbanpulse.ai/llms-full.txt'
  paymentGateways:
    default:
      description:
        en: Stripe-based API payment gateway
      type: Stripe
      version: 1
      reference: 'https://docs.stripe.com/'
      spec: |
        stripe.createCheckoutSession({
          amount: 4999,
          currency: 'usd',
          success_url: 'https://your-platform.com/success',
          cancel_url: 'https://your-platform.com/cancel'
        });
    agent:
      description:
        en: Payment gateway for AI agents
      type: Axio
      version: 1
      reference: 'https://www.x402.org/'
      spec: |
        paymentMiddleware("0xYourAddress", {"/mcp-access": "$0.01"});
  
  license:
    en:
      scope:
        definition: >-
          The purpose of this license is to determine the terms and conditions
          applicable to the licensing of the data product, whereby Data Holder
          grants Data User the right to use the data.
        restrictions: >-
          Data User agrees not to, directly or indirectly, participate in the
          unauthorized use, disclosure or conversion of any confidential
          information.
        geographicalArea:
          - EU
          - US
        permanent: false
        exclusive: false
        rights:
          - Reproduction
          - Display
          - Distribution
          - Adaptation
          - Reselling
          - Sublicensing
          - Transferring
      termination:
        noticePeriod: 90
        terminationConditions: >-
          After the expiry of the right of use, the product and its derivatives
          must be removed.
        continuityConditions: >-
          Expired license will automatically continued without written
          cancellation (termination) by Data Holder
      governance:
        ownership: >-
          Mindmote Oy, a company specializing in pet industry insights, owns the
          license to its proprietary data product 'Pets of the Year'.
        damages: >-
          During the term of license, except for the force majeure or the Data
          Holders reasons, Data User is required to follow strictly in
          accordance with the license. If Data User wants to terminate the
          license early, it needs to pay a certain amount of liquidated damages.
        confidentiality: >-
          Data User undertakes to maintain confidentiality as regards all
          information of a technical (such as, by way of a non-limiting example,
          drawings, tables, documentation, formulas and correspondence) and
          commercial nature (including contractual conditions, prices, payment
          conditions) gained during the performance of this license.
        applicableLaws: >-
          This license shall be interpreted, construed and enforced in
          accordance with the law of Finland, including Copyright Act 404/1961.
        warranties: >-
          Data Holder makes no warranties, express or implied, guarantees or
          conditions with respect to your use of the data product. To the extent
          permitted under local law, Data Holder disclaims all liability for any
          damages or losses, including direct, consequential, special, indirect,
          incidental or punitive, resulting from Data User use of the data
          product.
        audit: >-
          Data Holder will reasonably cooperate with Data Users by providing
          available additional information about the data product. Both parties
          will bear their own audit-related costs.
        forceMajeure: >-
          Both parties may suspend their contractual obligations when
          fulfillment becomes impossible or excessively costly due to
          unforeseeable events beyond their control, such as strikes, fires,
          wars, and other force majeure events.
  dataHolder:
    en:
      legalName: MindMote Oy
      businessId: 12243434-12
      email: contact@mindmote.fi
      taxID: 12243434-12
      vatID: 12243434-12
      logoURL: 'https://mindmote.fi/logo.png'
      description: Digital Economy services and tools
      URL: 'https://mindmote.fi'
      telephone: +35845 0232 2323
      streetAddress: Koulukatu 1
      postalCode: '33100'
      addressRegion: Pirkanmaa
      addressLocality: Tampere
      addressCountry: Finland
      aggregateRating: ''
      ratingCount: '1245'
      slogan: ''
      parentOrganization: ''


```
You'll find a complete machine-readbale example of a data product from the right column. It is imaginary data product *Urban Pulse* which contains derived data about events in the given city. The product has 4 pricing plans which are mostly based on recurring subscription model. Note! Not all voluntary attributes are used in the example and multilingualism has not been fully applied.
