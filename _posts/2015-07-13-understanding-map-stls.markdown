---
layout: post
title:  "Understanding MAP STL’s"
date:   2015-07-13 06:29:49
categories: map, c++, stl
banner_image: ""
featured: false
comments: true
---


<p>So you might have wondered what a MAP is? I am tyring to demystify it a bit, so pardon my technical way of putting it if its not so perfect! Its always best to think of any C++ related concept by taking an example from the real world. I have found that it always benefits me that way.</p>

<p>So lets take an office full of employees. Further more also lets assume that the employee ID is a unique number by which that employee is identifiable in that office. Now also lets have the following information about the employee</p>

<p>Age, Sex ,Address, First name, Last name – as parameters for identifying the employee in a more detailed fashion, and
Gross Salary, Net Salary and Tax per annum – as parameters for identifying the finances related to the employee.
Bear in mind that both these sets of data, are primarily associated with the employee ID. So now we can construct two sets of tables which have this data.</p>

<p><strong>Table 1:</strong></p>

<table>
<colgroup>
<col style="text-align:left;"/>
<col style="text-align:left;"/>
</colgroup>

<thead>
<tr>
	<th style="text-align:left;">Employee ID</th>
	<th style="text-align:left;">Identification information</th>
</tr>
</thead>

<tbody>
<tr>
	<td style="text-align:left;">1094</td>
	<td style="text-align:left;">32, Male ,771, Koramangala Layout, Bangalore City, Srikanth Eswaran</td>
</tr>
<tr>
	<td style="text-align:left;">2056</td>
	<td style="text-align:left;">35, Male, HSR Layout, Apartment 101, Bangalore City ,Kiran Vinayababu</td>
</tr>
</tbody>
</table>

<p><strong>Table 2:</strong></p>

<table>
<colgroup>
<col style="text-align:left;"/>
<col style="text-align:left;"/>
</colgroup>

<thead>
<tr>
	<th style="text-align:left;">Employee ID</th>
	<th style="text-align:left;">Salary information</th>
</tr>
</thead>

<tbody>
<tr>
	<td style="text-align:left;">1094</td>
	<td style="text-align:left;">$60000 (gross), $48000 (net), $10375 (tax)</td>
</tr>
<tr>
	<td style="text-align:left;">2056</td>
	<td style="text-align:left;">$120000 (gross), $70000 (net), $25000 (tax)</td>
</tr>
</tbody>
</table>

<p>So now what is it we can do to effectively not only store, BUT ALSO cross reference this information? We can use maps, not one, but two of them to put ease into the information access!</p>

<p><strong>MAP1: </strong>This is a map between a number and Identification information
<strong>MAP2: </strong>This is a map between a number and Salary information</p>

<pre><code>typedef map&lt;int  , identity&gt; Id2Identity; 
typedef map&lt;int  , salaryinfo&gt; Id2SalaryInfo;
</code></pre>

<p>So what is Identity? Its just a structure having column 2 of table 1.</p>

<p>And what about salaryInfo? Its just a structure having column 2 of table 2. Lets write it here:</p>

<pre><code>struct Identity
{
  unsigned int age;
  enum type
  {
    MALE, FEMALE
  }
  const char* address;
  const char* firstName;
  const char* lastName;
};

struct salaryInfo
{
  unsigned float grossSalary;
  unsigned float netSalary;
  unsigned float tax;
};
</code></pre>

<p>Having these two maps, its easy now to switch between the information from both these maps, based on the unique employee id associated with the data! We shall see how in a short while.</p>

<p>the “.first” and “.second” operators (if i may call them so) maybe used to access the values in the first and second column of the map respectively. So for eg., in the first map above,</p>

<pre><code>Id2Identity::iterator it;

it-&gt;first or (*it).first will give the employee ID

and it-&gt;second or (*it).second will give the structure containing identity details. for eg if we need the last name of the employee, then we say

it-&gt;second.lastName on the first record will be = “Eswaran”.
</code></pre>

<p>Having said this, now its easy to access the second column, if we have the first, by doing a find operation using the first column value. For eg., it-&gt;find(1094) on the first map will yield the structure having this data. So I can say it-&gt;find(1094).lastName and it will still return “Eswaran” </p>

<pre><code>- 32
- Male
- 771, Koramangala Layout, Bangalore City
- Srikanth
- Eswaran
</code></pre>

<p>Remember that the find operation is a O(log2(n)) operation compared to iterating through all the entries in the map on our own using an iterator, which is O(N).</p>

<p>So now it wont be difficult to find the tax of a person having an ID which you need to get if I would say that person’s last name is “Eswaran”. Try it, and you will soon feel maps are powerful and easy to use! More later!</p>