# Sample-SQL-extraction

** SQL query to create concatenated column when a specified condition is met

``` SQL
SELECT DISTINCT a.beneficiary_id
	,a.FileID
	,a.ActiveInactive
	,b.TypeCode
	,b.ActualDate [Date TIT]
	,MainAdrOrg.OfficialName [AuthAdd]
	,b.TypeOfPlace [PlaceType]
	,p.NameOfPlace [PlaceName]
	,b.TITPerp [TIT Perpetrator]
	,b.TITTransport
	,[TIT Org].OfficialOrg
	,CONCAT_WS(' / ', CASE 
			WHEN b.TITBK = 'Yes'
				THEN 'Best'
			END, CASE 
			WHEN b.TITElectric = 'Yes'
				THEN 'Electronic'
			END, CASE 
			WHEN b.TITForced = 'Yes'
				THEN 'Forced'
			END, CASE 
			WHEN b.TITHarsh = 'Yes'
				THEN 'Harsh'
			END, CASE 
			WHEN b.TITHuming = 'Yes'
				THEN 'Huming Bird'
			END, CASE 
			WHEN b.TITShacks = 'Yes'
				THEN 'Shaking'
			END, b.ITTTreaty) AS types_of_TIT
FROM Beneficiary a
LEFT JOIN Action b ON a.b_id = b.b_id
LEFT JOIN Place ON b.action_id = ActionPlace.action_id
LEFT JOIN Place p ON ActivityPlaceLink.place_id = p.place_id
LEFT JOIN FOrganization [TIT Org] ON b.TITPerpetrator = [TIT Org].organization_id
LEFT JOIN Figanization MainAdrOrg ON MainAdrOrg.organization_id = b.MainAddresseeResponsibleOfActivity
WHERE b.TypeCodeIN (
		'GI'
		,'IN'
		,'SIF'
		,'DQA'
		)
	AND b.TITTreat = 'yes'
	AND a.StarCode = 'operational'

```
