# Sharepoint-Sites-and-Users-Powershell 
Grabs Sharepoint Sites and Users in the sites and can be modified to grab other sharepoint sites as well. Just thought I'd share :D 

#Pre-reqs
Add-PSSnapin Microsoft.SharePoint.Powershell

#Will grab all SubSites and output
$spweb = Get-SPWeb "https://mysite.contoso.com/*" 

#Array to grab users and sites 
$array = @()
#$spweb = Get-SPSite 'https://mysite.contoso.com/' | Get-SPWeb -Limit All | Select Title, URL, SiteGroups, Name, AllUsers | Out-Host
$Groups = $SPWeb.SiteGroups            
Foreach ( $Group in $Groups ) {            
  $GroupName = $Group.Name              
   Foreach($User in $Group.users) {            
   $obj = New-Object PSObject -Property @{            
    GroupName = $GroupName            
    UserName = $User.Name 
    SiteName = $SPWeb.Url                       
      }            
  $array += $obj            
    }            
 }                    
$array     


