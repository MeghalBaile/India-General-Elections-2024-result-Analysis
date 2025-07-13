# India-General-Elections-Result-Analysis-2024

USE ELECTION_DB;


SELECT * FROM constituencywise_details;

SELECT * FROM constituencywise_results;

SELECT * FROM partywise_results;

SELECT * FROM statewise_results;

SELECT * FROM states;





--- PROBLEM STATEMENT :- 01  Total Seats

SELECT 
DISTINCT COUNT(Parliament_Constituency)
FROM constituencywise_results;



--- PROBLEM STATEMENT :- 02 What is the total number of seats available for elections in each state.

SELECT states.State AS StateName, COUNT(Constituency_ID) AS TotalSeatsAvailable
FROM states
JOIN statewise_results
	ON states.State_ID = statewise_results.State_ID
JOIN constituencywise_results
	ON constituencywise_results.Parliament_Constituency = statewise_results.Parliament_Constituency
GROUP BY 
		states.State
ORDER BY
		states.State;

--- PROBLEM STATEMENT :- 03 Total Seats Won by NDA Alliance

SELECT 
	SUM(CASE
		WHEN Party IN (
		'Apna Dal (Soneylal) - ADAL',
		'Asom Gana Parishad - AGP',
		'Bharatiya Janata Party - BJP',
		'Hindustani Awam Morcha (Secular) - HAMS',
		'Janasena Party - JnP',
		'Janata Dal  (Secular) - JD(S)',
		'Janata Dal  (United) - JD(U)',
		'Lok Janshakti Party(Ram Vilas) - LJPRV',
		'Nationalist Congress Party - NCP',
		'Rashtriya Janata Dal - RJD',
		'Rashtriya Lok Dal - RLD',	
		'Shiv Sena - SHS',
		'Sikkim Krantikari Morcha - SKM',
		'Telugu Desam - TDP'
		) THEN [won]
		ELSE 0
	END) AS NDA_Total_Seats_Won
FROM partywise_results

--- PROBLEM STATEMENT :- 04 Seats Won by NDA Alliance Party

SELECT 
	party AS PartyName,
	won AS SeatsWon
	FROM 
		partywise_results
	WHERE 
		party IN (
		'Apna Dal (Soneylal) - ADAL',
		'Asom Gana Parishad - AGP',
		'Bharatiya Janata Party - BJP',
		'Hindustani Awam Morcha (Secular) - HAMS',
		'Janasena Party - JnP',
		'Janata Dal  (Secular) - JD(S)',
		'Janata Dal  (United) - JD(U)',
		'Lok Janshakti Party(Ram Vilas) - LJPRV',
		'Nationalist Congress Party - NCP',
		'Rashtriya Janata Dal - RJD',
		'Rashtriya Lok Dal - RLD',	
		'Shiv Sena - SHS',
		'Sikkim Krantikari Morcha - SKM',
		'Telugu Desam - TDP'
		)
ORDER BY SeatsWon DESC;

--- PROBLEM STATEMENT :- 05 Total Seats Won by I.N.D.I.A Alliance Parties

SELECT
	SUM(CASE
		WHEN Party IN (
			'Aam Aadmi Party - AAAP',
			'All India Trinamool Congress - AITC',
			'Bharat Adivasi Party - BHRTADVSIP',
			'Communist Party of India  (Marxist) - CPI(M)',
			'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
			'Communist Party of India - CPI',
			'Dravida Munnetra Kazhagam - DMK',
			'Indian National Congress - INC',
			'Indian Union Muslim League - IUML',
			'Jammu & Kashmir National Conference - JKN',
			'Jharkhand Mukti Morcha - JMM',
			'Kerala Congress - KEC',
			'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
			'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
			'Rashtriya Loktantrik Party - RLTP',
			'Revolutionary Socialist Party - RSP',
			'Samajwadi Party - SP',
			'Shiromani Akali Dal - SAD',
			'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
			'Viduthalai Chiruthaigal Katchi - VCK'
			)THEN [won]
		ELSE 0
	END) AS NDA_Total_Seats_Won
FROM partywise_results;

--- PROBLEM STATEMENT :- 06 Seats Won by I.N.D.I.A Alliance Parties

SELECT 
	party AS PartyName,
	won AS SeatsWon
	FROM 
		partywise_results
	WHERE 
		party IN (
			'Aam Aadmi Party - AAAP',
			'All India Trinamool Congress - AITC',
			'Bharat Adivasi Party - BHRTADVSIP',
			'Communist Party of India  (Marxist) - CPI(M)',
			'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
			'Communist Party of India - CPI',
			'Dravida Munnetra Kazhagam - DMK',
			'Indian National Congress - INC',
			'Indian Union Muslim League - IUML',
			'Jammu & Kashmir National Conference - JKN',
			'Jharkhand Mukti Morcha - JMM',
			'Kerala Congress - KEC',
			'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
			'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
			'Rashtriya Loktantrik Party - RLTP',
			'Revolutionary Socialist Party - RSP',
			'Samajwadi Party - SP',
			'Shiromani Akali Dal - SAD',
			'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
			'Viduthalai Chiruthaigal Katchi - VCK'
		)
ORDER BY SeatsWon DESC;

--- PROBLEM STATEMENT :- 07 Add new column field in table partywise_results to get the Party Alliance as NDA, I.N.D.I.A and OTHER

ALTER TABLE partywise_results
ADD party_alliance VARCHAR(50)
 
UPDATE partywise_results
SET party_alliance = 'I.N.D.I.A'
WHERE party IN ( 
			'Aam Aadmi Party - AAAP',
			'All India Trinamool Congress - AITC',
			'Bharat Adivasi Party - BHRTADVSIP',
			'Communist Party of India  (Marxist) - CPI(M)',
			'Communist Party of India  (Marxist-Leninist)  (Liberation) - CPI(ML)(L)',
			'Communist Party of India - CPI',
			'Dravida Munnetra Kazhagam - DMK',
			'Indian National Congress - INC',
			'Indian Union Muslim League - IUML',
			'Jammu & Kashmir National Conference - JKN',
			'Jharkhand Mukti Morcha - JMM',
			'Kerala Congress - KEC',
			'Marumalarchi Dravida Munnetra Kazhagam - MDMK',
			'Nationalist Congress Party Sharadchandra Pawar - NCPSP',
			'Rashtriya Loktantrik Party - RLTP',
			'Revolutionary Socialist Party - RSP',
			'Samajwadi Party - SP',
			'Shiromani Akali Dal - SAD',
			'Shiv Sena (Uddhav Balasaheb Thackrey) - SHSUBT',
			'Viduthalai Chiruthaigal Katchi - VCK'
			);

UPDATE partywise_results
SET party_alliance = 'NDA'
WHERE party IN ( 
		'Apna Dal (Soneylal) - ADAL',
		'Asom Gana Parishad - AGP',
		'Bharatiya Janata Party - BJP',
		'Hindustani Awam Morcha (Secular) - HAMS',
		'Janasena Party - JnP',
		'Janata Dal  (Secular) - JD(S)',
		'Janata Dal  (United) - JD(U)',
		'Lok Janshakti Party(Ram Vilas) - LJPRV',
		'Nationalist Congress Party - NCP',
		'Rashtriya Janata Dal - RJD',
		'Rashtriya Lok Dal - RLD',	
		'Shiv Sena - SHS',
		'Sikkim Krantikari Morcha - SKM',
		'Telugu Desam - TDP'
		);

UPDATE partywise_results
SET party_alliance = 'OTHER'
WHERE party_alliance IS NULL;

---PROBLEM STATEMENT :- 08 Which party alliance (NDA, I.N.D.I.A, or OTHER) won the most seats across all states?

SELECT 
		party_alliance,
	SUM(won) AS Total
FROM partywise_results
GROUP BY party_alliance;

---PROBLEM STATEMENT :- 09 Winning candidate's name, their party name, total votes, and the margin of victory for a specific state and constituency?

SELECT constituencywise_results.Winning_Candidate,
	   partywise_results.Party,
	   constituencywise_results.Total_Votes,
	   constituencywise_results.Margin,
	   constituencywise_results.Constituency_Name,
	   partywise_results.party_alliance,
	   States.State
FROM constituencywise_results
JOIN partywise_results
	ON constituencywise_results.Party_ID = partywise_results.Party_ID
JOIN statewise_results
	ON constituencywise_results.Parliament_Constituency = statewise_results.Parliament_Constituency
JOIN States 
	ON statewise_results.State_ID = States.State_ID

---PROBLEM STATEMENT :- 10 What is the distribution of EVM votes for candidates in a specific constituency ?

SELECT constituencywise_details.Candidate,
	   constituencywise_details.Party,
	   constituencywise_details.EVM_Votes,
	   constituencywise_details.Postal_Votes,
	   constituencywise_details.Total_Votes,
	   constituencywise_results.Constituency_Name
FROM constituencywise_details
JOIN constituencywise_results
	ON constituencywise_details.Constituency_ID = constituencywise_results.Constituency_ID
ORDER BY constituencywise_details.Total_Votes DESC;

---PROBLEM STATEMENT :- 10 Which parties won the most seats in states.State, and how many seats did each party win?

SELECT partywise_results.Party,
	   COUNT(Constituency_ID) AS Seats_won
FROM partywise_results
JOIN constituencywise_results
	ON constituencywise_results.Party_ID = partywise_results.Party_ID
JOIN statewise_results
	ON statewise_results.Parliament_Constituency = constituencywise_results.Parliament_Constituency
JOIN states
	ON states.State_ID = statewise_results.State_ID
WHERE states.State = 'Andhra Pradesh'
GROUP BY partywise_results.Party
ORDER BY Seats_Won DESC;

---PROBLEM STATEMENT :- 11 What is the total number of seats won by each party alliance (NDA, I.N.D.I.A, and OTHER) in each state for the India Elections 2024

SELECT 
    states.State AS State_Name,
    SUM(CASE WHEN partywise_results.party_alliance = 'NDA' THEN 1 ELSE 0 END) AS NDA_Seats_Won,
    SUM(CASE WHEN partywise_results.party_alliance = 'I.N.D.I.A' THEN 1 ELSE 0 END) AS INDIA_Seats_Won,
	SUM(CASE WHEN partywise_results.party_alliance = 'OTHER' THEN 1 ELSE 0 END) AS OTHER_Seats_Won
FROM constituencywise_results
JOIN partywise_results
	ON constituencywise_results.Party_ID = partywise_results.Party_ID
JOIN statewise_results 
	ON constituencywise_results.Parliament_Constituency = statewise_results.Parliament_Constituency
JOIN states  
	ON statewise_results.State_ID = states.State_ID
WHERE partywise_results.party_alliance IN ('NDA', 'I.N.D.I.A',  'OTHER')  -- Filter for NDA and INDIA alliances
GROUP BY states.State
ORDER BY states.State;

---PROBLEM STATEMENT :- 12 Which candidate received the highest number of EVM votes in each constituency (Top 10)?

SELECT TOP 10
	   constituencywise_results.Constituency_ID,
	   constituencywise_results.Constituency_Name,
	   constituencywise_details.Candidate,
	   constituencywise_details.EVM_Votes
FROM constituencywise_details
JOIN constituencywise_results
	ON constituencywise_details.Constituency_ID = constituencywise_results.Constituency_ID
ORDER BY constituencywise_details.EVM_Votes DESC;

---PROBLEM STATEMENT :- 13 Which candidate won and which candidate was the runner-up in each constituency of State for the 2024 elections?

WITH RankedCandidates AS (
    SELECT 
        constituencywise_details.Constituency_ID,
        constituencywise_details.Candidate,
        constituencywise_details.Party,
        constituencywise_details.EVM_Votes,
        constituencywise_details.Postal_Votes,
        constituencywise_details.EVM_Votes + constituencywise_details.Postal_Votes AS Total_Votes,
        ROW_NUMBER() OVER (PARTITION BY constituencywise_details.Constituency_ID ORDER BY constituencywise_details.EVM_Votes + constituencywise_details.Postal_Votes DESC) AS VoteRank
    FROM constituencywise_details 
    JOIN constituencywise_results 
		ON constituencywise_details.Constituency_ID = constituencywise_results.Constituency_ID
    JOIN statewise_results 
		ON constituencywise_results.Parliament_Constituency = statewise_results.Parliament_Constituency
    JOIN states
		ON statewise_results.State_ID = states.State_ID
    WHERE states.State = 'Maharashtra'
)
SELECT 
    constituencywise_results.Constituency_Name,
    MAX(CASE WHEN RankedCandidates.VoteRank = 1 THEN RankedCandidates.Candidate END) AS Winning_Candidate,
    MAX(CASE WHEN RankedCandidates.VoteRank = 2 THEN RankedCandidates.Candidate END) AS Runnerup_Candidate
FROM RankedCandidates 
JOIN constituencywise_results
	ON RankedCandidates.Constituency_ID = constituencywise_results.Constituency_ID
GROUP BY constituencywise_results.Constituency_Name
ORDER BY constituencywise_results.Constituency_Name;

---PROBLEM STATEMENT :- 14 For the state of Maharashtra, what are the total number of seats, total number of candidates, total number of parties, total votes (including EVM and postal), and the breakdown of EVM and postal votes?

SELECT 
    COUNT(DISTINCT constituencywise_results.Constituency_ID) AS Total_Seats,
    COUNT(DISTINCT constituencywise_details.Candidate) AS Total_Candidates,
    COUNT(DISTINCT partywise_results.Party) AS Total_Parties,
    SUM(constituencywise_details.EVM_Votes + constituencywise_details.Postal_Votes) AS Total_Votes,
    SUM(constituencywise_details.EVM_Votes) AS Total_EVM_Votes,
    SUM(constituencywise_details.Postal_Votes) AS Total_Postal_Votes
FROM constituencywise_results 
JOIN constituencywise_details  
	ON constituencywise_results.Constituency_ID = constituencywise_details.Constituency_ID
JOIN statewise_results  
	ON constituencywise_results.Parliament_Constituency = statewise_results.Parliament_Constituency
JOIN states
	ON statewise_results.State_ID = states.State_ID
JOIN partywise_results 
	ON constituencywise_results.Party_ID = partywise_results.Party_ID
WHERE states.State = 'Maharashtra';
"# India-General-Elections-2024-result-Analysis" 
