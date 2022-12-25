## SET TOKENS:

In the beggining of the form (just below the <label>):
	<init>
	<unset token="selected_channel"></unset>
	</init>
In an input use <change>  
In a query use:
	<done>
	<progress>
	<finalized>
Set token based on conditions:
	Using IF or CASE
		<change>
		<!--Using IF-->
		<eval token="form.panel">if($time_difference$<=86400,"compare","single")</eval>
		<!--Using CASE-->
		<eval token="showPanelComparison">case($showPanel$=="Comparison","true")</eval>
		</change>
	Using CONDITION:
		<progress>
		<condition match="$master_token$==&quot;Data Entry&quot;">
		</progress>

	Using CONDITION on several conditions
		<condition match="''job.resultCount' > 0 AND result.custom_r1p1_vi'==&quot;line&quot;">

Access VALUE, RESULTS adn JOB on inputs:
	Access value:
		<change>
		<condition value="compare">
		<set token="showPanelComparison">true</set>
		</condition>
		</change>
	Empty value:
		<condition match="isnull($value$)"></condition>
	Search with no results:
		<condition match=" 'job.resultCount' != 0">
	Unset values from a form. Use both tokens below:
		<unset token="selected_channel"></unset>
		<unset token="form.selected_channel"></unset>