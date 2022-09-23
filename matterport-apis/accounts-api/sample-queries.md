# Sample Queries

Note that the Account API is available only with Enterprise Subscription tiers.  Interactive Console links will only be accessible to users logged into an Enterprise account.

### [Get organization info](https://api.matterport.com/api/accounts/graphiql/?operationName=getOrganizationInfo\&query=fragment%20developerInfo%20on%20DeveloperAccount%20%7B%0A%20%20mode%0A%20%20license%20%7B%0A%20%20%20%20availability%0A%20%20%7D%0A%7D%0A%0Afragment%20sdkKey%20on%20SdkKey%20%7B%0A%20%20key%0A%20%20label%0A%20%20domains%20%7B%0A%20%20%20%20created%0A%20%20%20%20secureOnly%0A%20%20%20%20domain%0A%20%20%20%20port%0A%20%20%7D%0A%7D%0A%0Afragment%20sdkKeyInfo%20on%20SdkKeyDetails%20%7B%0A%20%20used%0A%20%20remaining%0A%20%20quota%0A%20%20keys\(active%3A%20true\)%20%7B%0A%20%20%20%20...sdkKey%0A%20%20%7D%0A%7D%0A%0Afragment%20bundleInfo%20on%20OrganizationBundle%20%7B%0A%20%20id%0A%20%20name%0A%20%20description%0A%20%20enabled%0A%7D%0A%0Aquery%20getOrganizationInfo%20%7B%0A%20%20organization%20%7B%0A%20%20%20%20name%0A%20%20%20%20created%0A%20%20%20%20developer%20%7B%0A%20%20%20%20%20%20...developerInfo%0A%20%20%20%20%7D%0A%20%20%20%20sdkKeys%20%7B%0A%20%20%20%20%20%20...sdkKeyInfo%0A%20%20%20%20%7D%0A%20%20%20%20bundles%20%7B%0A%20%20%20%20%20%20...bundleInfo%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A) <a href="#get-organization-info" id="get-organization-info"></a>

Fragments can be mixed and matched depending on which data you want. The organization ID is based on which API tokens are used.\
\
Sample Return

```json
{ 
   "data": { 
      "organization": { 
         "name": "Matterport Organization", 
         "created": "2020-11-03T21:43:39Z", 
         "developer": { 
            "mode": "production", 
            "license": { 
               "availability": "unlocked" 
            } 
         }, 
         "sdkKeys": { 
            "used": 1, 
            "remaining": 4, 
            "quota": 5, 
            "keys": [ 
               { 
                  "key": "XXXXXXXXXXXXXXXXXX", 
                  "domains": [ 
                     { 
                        "created": "1605138155932", 
                        "secureOnly": false, 
                        "domain": "localhost" 
                     } 
                  ] 
               }, 
            "bundles": [ 
               { "id": "mp:matterpak", 
               "name": "Matterpak", 
               "description": "Order high resolution assets associated with the model.", 
               "enabled": true 
            }, 
            { 
               "id": "cubicasa:floorplan", 
               "name": "Cubicasa Schematic Floorplan", 
               "description": "Order an enhanced schematic floorplan", 
               "enabled": true 
            }, 
            { 
               "id": "trueplan:schematic", 
               "name": "TruePlan™ Schematic", 
               "description": "Order a TruePlan™ Schematic", 
               "enabled": false 
            }, 
            { 
               "id": "gsv:publish", 
               "name": "Google Street View", 
               "description": "Publish to Google Street View", 
               "enabled": true 
            }, 
            { 
               "id": "homeaway:publish", 
               "name": "Vrbo - HomeAway", 
               "description": "Create a 360 Tour for Vrbo and HomeAway",
               "enabled": true 
            } 
         ] 
      } 
   } 
}
```

### [Get organization members info](https://api.matterport.com/api/accounts/graphiql/?operationName=getOrganizationInfo\&query=fragment%20user%20on%20User%7B%0A%20%20id%0A%20%20firstName%0A%20%20lastName%0A%20%20email%0A%20%20created%0A%7D%0A%0Aquery%20getOrganizationInfo%20%7B%0A%20%20organization%20%7B%0A%09%09memberships\(%0A%20%20%20%20%20%20query%3A%20%22\*%22%2C%0A%20%20%20%20%20%20pageSize%3A%20100%2C%0A%20%20%20%20%20%20offset%3A%20null%0A%20%20%20%20\)%7B%0A%20%20%20%20%20%20nextOffset%2C%0A%20%20%20%20%20%20results%7B%0A%20%20%20%20%20%20%20%20user%20%7B%0A%20%20%20%20%20%20%20%20%20%20...user%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20roles%7B%0A%20%20%20%20%20%20%20%20%20%20id%0A%20%20%20%20%20%20%20%20%20%20name%0A%20%20%20%20%20%20%20%20%7D%0A%20%20%20%20%20%20%20%20status%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A) <a href="#get-organizations-members-info" id="get-organizations-members-info"></a>

Results might need to be [paginated](https://graphql.org/learn/pagination/#pagination-and-edges) (offset pagination).\
\
Sample Return

```json
{ 
   "data": {
      "organization": {
         "memberships": {
            "results": [
               {
                  "user": {
                     "id": "XXXXXXXXXXX",
                     "firstName": "XXX",
                     "lastName": "XXXXXXX",
                     "email": "XXXXXX@XXXXXX.com",
                     "created": "2020-11-03T21:43:39Z"
                  },
                  "roles": [
                     {
                        "id": "00000000200",
                        "name": "owner"
                     },
                     {
                        "id": "00000000080",
                        "name": "billing-admin"
                     },
                     {
                        "id": "00000000120",
                        "name": "admin"
                     }
                  ],
                  "status": "active"
               },
               {
                  "user": {
                     "id": "XXXXXXXXXXX",
                     "firstName": "XXX",
                     "lastName": "XXXXXXX",
                     "email": "XXXXXXX@XXXXX.com",
                     "created": "2022-05-03T22:05:00Z"
                  },
                  "roles": [
                     {
                        "id": "00000000120",
                        "name": "admin"
                     }
                  ],
                  "status": "active"
               },
               {
                  "user": {
                  "id": "XXXXXXXXXXX",
                  "firstName": "XXX",
                  "lastName": "XXXXXXX",
                  "email": "XXXXXXX@XXXXX.com",
                  "created": "2021-03-09T20:33:57Z"
               },
               "roles": [
                  {
                     "id": "00000000100",
                     "name": "collaborator"
                  }
               ],
               "status": "active"
            },
         ]
      }
   }
}
```

### [Invite user to organization](https://api.matterport.com/api/accounts/graphiql/?operationName=inviteUser\&query=%23%20Role%20ID%20reference%3A%0A%23%20collaborator%20%3D%2000000000100%0A%23%20admin%20%3D%2000000000120%0A%23%20owner%20%3D%2000000000200%0A%23%20billing-admin%20%3D%2000000000080%0A%0A%0Amutation%20inviteUser\(%24userEmail%3A%20String!%2C%20%24roleId%3A%20ID!%2C%20%24inviteMessage%3A%20String\)%7B%0A%20%20%0A%20%20inviteMember\(%0A%20%20%20%20email%3A%20%24userEmail%0A%20%20%20%20roleId%3A%20%24roleId%0A%20%20%20%20inviteMessage%3A%20%24inviteMessage%0A%20%20\)%7B%0A%20%20%20%20user%7Bemail%7D%0A%20%20%20%20status%0A%20%20%7D%0A%7D%0A\&variables=%7B%0A%20%20%22userEmail%22%3A%20%22%22%2C%0A%20%20%22roleId%22%3A%20%22%22%0A%7D) <a href="#invite-user-to-organization" id="invite-user-to-organization"></a>

Sample Return

```json
{ 
   "data": { 
      "inviteMember": { 
         "user": { 
            "email": "XXXXXXX@XXXXX.com" 
         }, 
         "status": "pending" 
      } 
   } 
}
```

### [Remove user from organization](https://api.matterport.com/api/accounts/graphiql/?operationName=removeMember\&query=mutation%20removeMember\(%24email%3A%20String!\)%7B%0A%20%20removeMembership\(email%3A%20%24email\)%7B%0A%20%20%20%20user%7Bemail%7D%0A%20%20%20%20status%0A%20%20%7D%0A%7D\&variables=%7B%0A%20%20%22email%22%3A%20%22%22%0A%7D) <a href="#remove-user-from-organization" id="remove-user-from-organization"></a>

Sample Return

```json
{ 
   "data": { 
      "removeMembership": { 
         "user": { 
            "email": "XXXXXXX@XXXXX.com" 
         }, 
         "status": "deleted" 
      } 
   } 
}
```

### [Update a user's role](https://api.matterport.com/api/accounts/graphiql/?operationName=updateUserRole\&query=%23%20Role%20ID%20reference%3A%0A%23%20collaborator%20%3D%2000000000100%0A%23%20admin%20%3D%2000000000120%0A%23%20owner%20%3D%2000000000200%0A%23%20billing-admin%20%3D%2000000000080%0A%0Amutation%20updateUserRole\(%24email%3A%20String!%2C%20%24roleId%3A%20ID!\)%7B%0A%20%20patchMembership\(email%3A%20%24email%2C%20roleId%3A%20%24roleId\)%7B%0A%20%20%20%20user%7Bemail%7D%0A%20%20%20%20roles%7B%0A%20%20%20%20%20%20id%0A%20%20%20%20%20%20name%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A\&variables=%7B%0A%20%20%22email%22%3A%20%22%22%2C%0A%20%20%22roleId%22%3A%20%22%22%0A%7D) <a href="#update-a-users-role" id="update-a-users-role"></a>

Sample Return

```json
{ 
   "data": { 
      "patchMembership": { 
         "user": { 
            "email": "XXXXXXX@XXXXX.com" 
         }, 
         "roles": [ 
            { 
               "id": "00000000100", 
               "name": "collaborator" 
            } 
         ] 
      } 
   } 
}
```

### SDK Key management <a href="#sdk-key-management" id="sdk-key-management"></a>

* [List SDK Keys](https://api.matterport.com/api/accounts/graphiql/?operationName=getSDKKeys\&query=fragment%20keyInfo%20on%20SdkKey%7B%0A%20%20key%0A%20%20domains%7B%0A%20%20%20%20secureOnly%0A%20%20%20%20domain%0A%20%20%20%20port%0A%20%20%7D%0A%7D%0A%0Aquery%20getSDKKeys%7B%0A%20%20organization%7B%0A%20%20%20%20sdkKeys%7B%0A%20%20%20%20%20%20quota%0A%20%20%20%20%20%20used%0A%20%20%20%20%20%20remaining%0A%20%20%20%20%20%20keys%7B%20...keyInfo%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D)
* [Add SDK Key](https://api.matterport.com/api/accounts/graphiql/?operationName=addSdkKey\&query=fragment%20sdkKey%20on%20SdkKey%7B%0A%20%20key%0A%20%20label%0A%20%20domains%7B%0A%20%20%20%20secureOnly%0A%20%20%20%20domain%0A%20%20%7D%0A%7D%0A%0Amutation%20addSdkKey\(%24label%3A%20String%2C%20%24domains%3A%20%5BAddSdkDomain!%5D\)%7B%0A%20%20provisionSdkKey\(%0A%20%20%20%20label%3A%20%24label%0A%20%20%20%20domains%3A%20%24domains%0A%20%20\)%7B%0A%20%20%20%20...sdkKey%0A%20%20%7D%0A%7D\&variables=%7B%0A%20%20%22label%22%3A%20%22My%20SDK%20Key%22%2C%0A%20%20%22domains%22%3A%20%5B%0A%20%20%20%20%7B%0A%20%20%20%20%20%20%22domain%22%3A%20%22http%3A%2F%2Flocalhost%22%2C%0A%20%20%20%20%20%20%22secureOnly%22%3A%20false%2C%0A%20%20%20%20%20%20%22port%22%3A%208000%0A%20%20%20%20%7D%0A%20%20%5D%0A%7D)
* [Delete SDK Key](https://api.matterport.com/api/accounts/graphiql/?operationName=removeSdkKey\&query=mutation%20removeSdkKey\(%24key%3A%20ID!\)%7B%0A%20%20removeSdkKey\(key%3A%20%24key\)%0A%7D\&variables=%7B%0A%20%20%22key%22%3A%20%22%22%0A%7D)
* [Add domain to SDK key](https://api.matterport.com/api/accounts/graphiql/?operationName=addDomain\&query=mutation%20addDomain\(%24key%3A%20ID!%2C%20%24domainDetails%3A%20AddSdkDomain!\)%7B%0A%20%20addSdkDomain\(key%3A%20%24key%2C%20details%3A%20%24domainDetails\)%7B%0A%20%20%20%20domain%0A%20%20%20%20secureOnly%0A%20%20%7D%0A%7D\&variables=%7B%0A%20%20%22key%22%3A%20%22%22%2C%0A%20%20%22domainDetails%22%3A%20%7B%0A%20%20%20%20%22domain%22%3A%20%22http%3A%2F%2Flocalhost%22%2C%0A%20%20%20%20%22secureOnly%22%3A%20false%2C%0A%20%20%20%20%22port%22%3A%208000%0A%20%20%7D%0A%7D)
* [Remove domain on SDK key](https://api.matterport.com/api/accounts/graphiql/?operationName=removeDomain\&query=mutation%20removeDomain\(%24key%3A%20ID!%2C%20%24domainId%3A%20ID!\)%7B%0A%20%20removeSdkDomain\(key%3A%20%24key%2C%20domainId%3A%20%24domainId\)%0A%7D\&variables=%7B%0A%20%20%22key%22%3A%20%22%22%2C%0A%20%20%22domainId%22%3A%20%22%22%0A%7D)
* [Update domain on SDK key](https://api.matterport.com/api/accounts/graphiql/?operationName=updateDomain\&query=mutation%20updateDomain\(%24key%3A%20ID!%2C%20%24domainId%3A%20ID!%2C%20%24newInfo%3A%20PatchSdkDomain!\)%7B%0A%20%20patchSdkDomain\(key%3A%20%24key%2C%20domainId%3A%20%24domainId%2C%20patch%3A%20%24newInfo\)%7B%0A%20%20%20%20id%0A%20%20%20%20secureOnly%0A%20%20%20%20domain%0A%20%20%20%20port%0A%20%20%7D%0A%7D\&variables=%7B%0A%20%20%22key%22%3A%20%22%22%2C%0A%20%20%22domainId%22%3A%20%22%22%2C%0A%20%20%22newInfo%22%3A%20%7B%0A%20%20%20%20%22domain%22%3A%20%22http%3A%2F%2Flocalhost%22%2C%0A%20%20%20%20%22secureOnly%22%3A%20false%2C%0A%20%20%20%20%22port%22%3A%206000%0A%20%20%7D%0A%7D)
