# Pricing Analysis and Revenue Management Case Study

## Case Study Introduction
Copa Cruises is a 40-year old company that offers dining and sightseeing cruises. What started with only one ship at Maryland’s Eastern Shore, is now a big business operating at multiple locations with 40 vessels.

Copa operates scheduled tours at least twice daily during the peak travel/tourism seasons at each of its locations. The total number of scheduled tours varies based on the number of vessels available at each location.

Copa also offers its ships exclusively for groups. In fact, a significant portion of Copa’s revenues come from group bookings. Typically, group customers book for corporate events, weddings, or private celebrations (e.g. family reunion). Copa customizes the table arrangement, the deck, and the menu to suit its customers’ needs for a group event. An event coordinator helps customers with the layout, food and dining options, and other special needs for their utmost satisfaction. The event coordinators at each of the locations oversee reservations and logistics of special events.

Currently, event coordinators have full responsibility in pricing the cruises for groups. Once a customer makes an inquiry, an event coordinator first checks the availability by date. If the group can be accommodated given the capacity of a ship and there is availability for the desired date, further information about the event is gathered. A service contract that specifies the date, time, route and length of the cruise, the food and beverage selection, and additional service needs, is prepared. The event coordinator specifies a price per person to cover all the expenses of a tour in this contract. Information on each contract is recorded in Copa’s database.

Event coordinators charge different prices to different customers. However, price differentiation is done in an ad hoc manner. Each coordinator relies on his/her expertise and knowledge to quote a price to a customer. Many event coordinators think corporate groups are less sensitive to prices compared to private groups. Others think there are geographic differences: A private event is believed to be more likely to accept a contract with a higher price in New York City compared to other locations. In summary, there seems to be systematic biases at pricing group events.

Copa is interested in providing guidance to its event coordinators to make better pricing decisions. Contract data that has been collected for a 12-month duration will be used for this purpose. Table-1 below shows a snapshot of data. Each transaction has a unique Customer-ID. The event takes place at a specific location, denoted by a number (e.g. location 1 is Boston). Information on how far in advance the booking was made, the type of event (wedding, private or business), the price (per person) quoted to the customer, and whether the customer booked the cruise at that price (recorded in the “Win” column; a 1 indicates customer booked the cruise, 0 indicates otherwise) are all recorded in the data file.

| Customer | ID Location | Booking Date (# of days before the event) | Type    | Price Quote ($ per person) | Win |
|----------|-------------|-------------------------------------------|---------|---------------------------|-----|
| 2007-1   | 8           | 47                                        | Wedding | $179.00                   | 0   |
| 2007-2   | 10          | 195                                       | Private | $118.00                   | 1   |
| 2007-3   | 6           | 84                                        | Private | $180.00                   | 0   |
| 2007-5   | 1           | 177                                       | Wedding | $157.00                   | 1   |
Table-1: Snapshot of collected data.

The list of locations is also available in the data file. All the events recorded in the data set were for groups of size 50. The groups were homogeneous in their needs such as the length of the tour and the type of service provided on board. In other words, the cost of the cruise did not vary across customers included in this data set.

Dataset Link - https://github.com/ChidubemJP/Pricing-Analysis-Revenue-Management/blob/main/Copa-Data-File-1.xls
---

## Problem Statement

### Assume that Copa charges a single price per person for all events.

**(a) What is the price (per person) that maximizes expected revenue per event for Copa? What is the expected revenue per transaction for that price?**

**Methodology**

Assumption: Copa charges a single price per person for all events.

From the structure of the provided data, I observed that it had a similar format to that of a bid-response model, i.e., in addition to the information about the contracts, it contained a Quote column, and a 0-1 Win column. To estimate an expected revenue maximizing price, I first calculated the Bid Response Function, or the Probability of booking the customer at quoted price p:

W(p) = 1 / [ 1 + EXP(a+bp)]

Since I am looking for a single price per person in this analysis, I focused only on the Quote and Win columns. I fit the logit model with the given data and calculated the Probability(Win) and Probability(Loss) to calculate the Maximum Likelihood estimation of winning. Then I assumed an arbitrary starting value of decision variables a and b, and created and solved the following Solver model to maximize ln(likelihood) with constraints: **a <= 0; b >= 0.**


1. Determine the single optimal price per person that maximizes expected revenue.
2. Identify optimal pricing strategies for different market segments (event types and geographic locations).

---

## Methodology
### Data Analysis Approach
- The dataset was treated as a bid-response model.
- A logistic regression model was applied to calculate the probability of booking (`W(p)`).

### Revenue Maximization
- Expected revenue per transaction was calculated as:
