# Election Audit Results with Python

Data analysis using Python is cleaner and provides better version control than VBA in Excel. Python is faster than Excel for data pipelines, automation and calculating complex equations and algorithms. Python is open-source, consistent and accurate in the execution of code, so its easy for any users to replicate or modify the original code in future.

## Overview of Project

Tom is a **Colorado Board of Elections** Employee who is doing the **Election Audit** for Colorado Congressional District Election. So, we have a list of data with "Ballot ID, County and Candidate Name". Tom and his manager Seth is interested to find the below details out of the election result data.

  •	Total number of votes cast

  •	Candidates with their total and percentages of vote received
  
  •	Each County's total and percentage of votes 
  
  •	Largest turnout County based on total votes 
  
  •	The winner of the election based on popular vote
 
### Purpose

Tom wants to perform the Analysis based on County as well as Candidates and it will be easy for him to do it with Python. He need to submit the Election Audit results to Election Board, so having the results in text file and displaying in the terminal makes the work easy and clean. 

Also, he may want to refactor the script to make it generic for any election. 

## Analysis 

As there are large number of data for many candidates, counties and each have corresponding vote counts, we may need to create a list, dictionories to store and use in the program. Also, inititalizing all the variable is also important.

![PyPoll_Challenge_Arrays](https://github.com/saranyadurairaju/Module3-Final-Assignment-Analysis/blob/main/PyPoll_Challenge_Arrays.png)

* When we are reading through the row of datas, we need to get the unique Candidate names and count their corresponding votes. Once we find the next unique candidate, we need to initialize the Votes count and start counting for the new candidate. Below is the piece of code, with condition statement to perform this logic.


       if candidate_name not in candidate_options:
            # Add the candidate name to the candidate list.
            candidate_options.append(candidate_name)

            # And begin tracking that candidate's voter count.
            candidate_votes[candidate_name] = 0
            
       Add a vote to that candidate's count
       candidate_votes[candidate_name] += 1


* As like the Candidates, we need to get the County list and the Votes registered in each County.

![PyPoll_Challenge_County](https://github.com/saranyadurairaju/Module3-Final-Assignment-Analysis/blob/main/PyPoll_Challenge_County.png)

* Once the Votes are counted for each candidate and county, we need to write the result in terminal as well as in a separate text file for Election Commission.

      for candidate_name in candidate_votes:
          # Retrieve vote count and percentage
          votes = candidate_votes.get(candidate_name)
          vote_percentage = float(votes) / float(total_votes) * 100
          candidate_results = (
              f"{candidate_name}: {vote_percentage:.1f}% ({votes:,})\n")

          # Print each candidate's voter count and percentage to the terminal.
          print(candidate_results)
          #  Save the candidate results to our text file.
          txt_file.write(candidate_results)

* For County calculations, we need to perform the same checking and write the result in the output file. Below is the code for County: 

![PyPoll_Challenge_Write_County](https://github.com/saranyadurairaju/Module3-Final-Assignment-Analysis/blob/main/PyPoll_Challenge_write_County.png)

* Finally we need to write the Winning candidate details in the terminals and the output text file:

  **Determine winning vote count, winning percentage, and candidate.**

          if (votes > winning_count) and (vote_percentage > winning_percentage):
              winning_count = votes
              winning_candidate = candidate_name
              winning_percentage = vote_percentage

  **Print the winning candidate (to terminal).**

          winning_candidate_summary = (
              f"-------------------------\n"
              f"Winner: {winning_candidate}\n"
              f"Winning Vote Count: {winning_count:,}\n"
              f"Winning Percentage: {winning_percentage:.1f}%\n"
              f"-------------------------\n")
          print(winning_candidate_summary)
          # Save the winning candidate's name to the text file
          txt_file.write(winning_candidate_summary)

Performing the calculations and writing the report in the above methods will give us the **Election Audit** results in the terminal as well as in the **Election_results** text file for Election Commission.

## Challenges

* Finding the correct way to automate the whole process and getting the result with a minimum run time is little challenging. But this helps us to try doing the things in many ways, which results in better solution. 

* We have to make sure the data is sorted in proper order to find the unique Candidates, Counties and Votes.

## Results

Below is the full Python code to determine the Election results. 

![PyPoll_Challenge](https://github.com/saranyadurairaju/Module3-Final-Assignment-Analysis/blob/main/PyPoll_Challenge.py)

The total Votes cast in the Congressional Election is **369,711**
 
#### The County-wise Results

After the execution of the above mentioned Python program, we will get the county results as follows:

	County Votes:
	Jefferson: 10.5% (38,855)
	Denver: 82.8% (306,055)
	Arapahoe: 6.7% (24,801)

  So, Jefferson County received 10.5% and Arapahoe received 6.7% of the total votes. But Denver has 82.8% votes cast in the Congressional Election. 
  
	  ---------------------------------------
	     Largest County Turnout: Denver
  	---------------------------------------

#### The Candidate-wise Results

Below is the Candidates details with their corresponding number of Votes and Percentage of Votes in the Election.

	Charles Casper Stockham: 23.0% (85,213)
	Diana DeGette: 73.8% (272,892)
	Raymon Anthony Doane: 3.1% (11,606)

* Raymon got a least number of 11,606 votes in total, which is a 3.1%

* Another Candidate Charles received a 23% of votes with a total of 85,213.

* Diana DeGette got a maximum number of votes, with 73.8% and 272,892 in total.

### The Winner of the Election

_From the above percentage and total number of Votes, its clear that **Diana DeGette** won the Election and **Denver** county had a maximum Votes._
 
	Winner: Diana DeGette
	Winning Vote Count: 272,892
	Winning Percentage: 73.8% 	

The complete Election Audit results will be printed in the Terminal. Also, the same results will be saved in **election_analysis.txt** file in "analysis" folder.

**The Election Results Saved to a Text File**

![PyPoll_election_analysis](https://github.com/saranyadurairaju/Module3-Final-Assignment-Analysis/blob/main/analysis/election_analysis.txt)



**The Election Results Printed to the Command Line**

![PyPoll_Challenge_Terminal](https://github.com/saranyadurairaju/Module3-Final-Assignment-Analysis/blob/main/PyPoll_Challenge_Terminal.png)

## Summary

### Common Script for Elections

Code modification is a way of restructuring and optimizing existing code to give results for multiple elections without changing its behavior and results. It is a way to improve the code quality, saving time and money. 

**United States presidential election**

This same script can be modified and used for Presidential Election 

- Create another column with State name
- Need to find the county-wise winning candidate by using the dictionary
- Then have to find the State winner by comparing the county result
- whoever get the maximum county, will get the total State counts.
- Winner will be announced based on the maximum State counts.

**Multiple-choice referendums**

For referendum it will be little different. But we can easily modify the same logic.

- Here we will have referendum questions 
- And corresponding "Yes" or "No" answers
- For each questions we need to calculate the counts
- Compare the total counts of yes or no
- The result can be easily made out of the comparison  

**User Interface to view the results**

The above Congressional Election script can be modified such a way that any User can provide either the Candidate name or County name to see the results. In this way, during the bigger election with many number of results, any user can find the result for whichever county or candidate they are interested. 


_Tom and his manager Seth can provide a nice and perfect **Election Audit** results to the Election Commission with a extra points to make the code generic. Hurry!!!_
