# White Paper: Sustainable Grant Funding and Bounty System

## Introduction

In an effort to enhance the robustness and reliability of scientific research, our organization has developed a unique funding model that integrates a self-sustaining financial structure with a rigorous validation mechanism through a bounty system. This white paper outlines the key features of this model, its financial strategy, sustainability mechanisms, and the benefits it offers to the research community and funding bodies.

## Model Overview

The grant funding model is designed to be self-sustaining by leveraging interest earned on an initial endowment to fund research grants and bounties for disproving existing studies. The primary goals are to encourage rigorous scientific inquiry and provide a financial structure that maintains its value against inflation and increases funding capacity over time.

### Initial Setup

The system starts with an initial endowment, referred to as the "seed," which is set at $5,000,000. The seed amount is invested, and the interest generated is used to fund ongoing operations:

- **Interest Rate**: The annual nominal interest rate is set at 8%.
- **Grant Awards**: Each year, 1/4 of the interest accrued is allocated to fund new grants.
- **Reinvestment**: The remaining 3/4 of the interest is reinvested to ensure growth and sustainability of the fund.

### Bounty System

A critical component of the model is the bounty system, which offers financial rewards for disproving previously funded studies. This system is designed to ensure that only robust, reproducible research is rewarded in the long term:

- **Bounty Calculation**: The bounty amount is calculated based on the difference between the current fund amount and a risk-adjusted projection of the seed, distributed equally among up to three valid disprovers.
- **Risk Adjustment**: The risk-free rate used for projections is half the nominal interest rate, acknowledging the lower risk associated with proven, stable investments.

Adjudicating the bounty system would somewhat inevitably be a bit of a contentious process, though the author believes this is something the community and/or organizations like NSF/NIH/DARPA could figure out. Some example proposals would be: 1) to require blind/hidden bug-bounty submissions, and 2) only adjudicated if 3-independent methods disprove the result (e.g. one shows methodological errors in the actual data, one shows a mechanistic problem in the underlying phenomena [i.e. cell X can’t absorb Y in Petri dish, so that same conclusion in human body must be false], etc.

*We should, as a field, recognize that this has roughly been able to be succesfully conducted towards software security.* While software security is provable through valid Proofs-of-Concept (POCs) and exploit code, in a way that a cell-mechanism or a quantum interaction might be much harder to show, it is still a decent North Star for reasoning about how such a system might work.

### Sustainability and Growth

The model is structured to grow over time, with each disproving event resetting the fund to a higher baseline amount than the original seed, adjusted for accrued interest and less the total bounty paid. This adjustment protects the fund against inflation and increases its grant-awarding capacity. Over the course of 20 years, if started today, a PI could expect to receive more than $3.6 million for a result that holds. A successful result could be paid out for an extremely large period, say 40 years, where after year 20, all money would be paid directly to the PI's institution. This could have the effect of encouraging institutions to put more emphasis in their selection and facilitation of PIs who are most likely to produce long-term reproducible scientific results.

### Background on Current Government R&D Funding in the United States

Here is a figure from a [GAO Report on 2021 Funding](https://www.gao.gov/products/gao-23-105396).

![Federal Research and Development Obligations, Fiscal Year 2021](https://www.gao.gov/assets/extracts/e02d5c69b698c49e644b6a679888383c/rId13_image2.png)

In fiscal year 2021, industry, universities, and colleges received the majority of these external R&D obligations—almost **$90 billion.**

*While a large part of this money may have gone <u>to development</u>*, i.e. building the F35, it is easy to imagine that something like $100 million could be used to create a robust pilot program with 20 seed grants with \$50 million [^1] set aside for administration costs, and this would amount to being just 2% of [DARPA's 2024 budget](https://www.darpa.mil/about-us/budget-and-finance#:~:text=The%20President's%20FY2025%20budget%20request,Congressional%20testimony%20by%20DARPA%20leadership.).

[^1]: Typical "overhead" rates at US Universities and Private Sector R&D range from 35-69%.

## Financial Strategy and Implementation

The following Python code snippet illustrates the implementation of the funding model, capturing the annual operations, grant awards, and bounty calculations over a 20-year period:

```python
# Initial seed and setup parameters
seed = 5e6  # Initial seed amount in dollars
interest_rate = .08  # Annual nominal interest rate

# Dictionary to hold details of each year's operations
outcomes_dict = {"amount": seed}
outcomes = []  # List to store yearly outcomes

for i in range(20):  # Loop over 20 years to simulate the fund operations
    outcomes_dict["annual_award"] = int(outcomes_dict["amount"] * (interest_rate / 4))  # Calculate annual grant
    outcomes_dict["amount"] = int(outcomes_dict["amount"] * (1 + interest_rate * 3 / 4))  # Reinvest the remaining interest
    outcomes_dict["year"] = i  # Record the year
    outcomes_dict["possible_bounty"] = int((outcomes_dict["amount"] - seed * (1 + interest_rate / 2) ** i) / 3)  # Calculate possible bounty
    outcomes_dict["new_starting_point"] = int(outcomes_dict["amount"] - outcomes_dict["possible_bounty"] * 3)  # Adjust fund for next year
    outcomes.append(outcomes_dict)  # Append the year's outcome to the list
    amount = outcomes_dict["amount"]
    outcomes_dict = {"amount": amount}  # Reset dictionary for the next year
```

## Example Outcomes

This table shows example outcomes from the code above for the first five years.

| Year | Amount Accrued | Annual Award | Possible Bounty | New Grant Starting Point | Amount Received by PI if Results Hold |
| ---: | -------------: | -----------: | --------------: | -----------------------: | ------------------------------------: |
|    0 |        5300000 |       100000 |          100000 |                  5000000 |                                100000 |
|    1 |        5618000 |       106000 |          139333 |                  5200001 |                                206000 |
|    2 |        5955080 |       112360 |          182359 |                  5408003 |                                318360 |
|    3 |        6312384 |       119101 |          229354 |                  5624322 |                                437461 |
|    4 |        6691127 |       126247 |          280611 |                  5849294 |                                563708 |

## Benefits

The benefits of this innovative funding model include:

- **Enhanced Research Integrity**: By incentivizing the disproval of studies, the model promotes a high standard of scientific integrity and rigor.
- **Financial Sustainability**: The model's reinvestment strategy ensures that the fund grows over time, enhancing its capability to support larger or more numerous grants.
- **Adaptability to Economic Changes**: The fund's structure allows for adjustments based on economic conditions, ensuring its long-term viability.

## Conclusion

Our sustainable grant funding and bounty system represents a forward-thinking approach to research financing, emphasizing accountability, sustainability, and growth. By implementing this model, funding bodies can ensure that they are not only supporting high-quality research but also fostering an environment where scientific findings are continuously validated, thereby advancing the knowledge base in a financially prudent manner.

