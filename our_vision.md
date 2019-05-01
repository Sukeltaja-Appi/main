## Start
Basic idea was to create a social tool for divers diving in finland. **MVP requirements** were to have a working app, with possibility to search and select locations for diving events, share events and photos. 

#### List of things we didn't manage to add.
* Photo services (profile / sharing etc.)
* Personal messaging?
* Logging in with Sukeltajaliitto (and services for Sukeltajaliitto-profile)


##### About the models we created
   The Event subject grew during the process and ended up being greater than it was planned at the beginning. 
* Event now contains three diffrent user types: Creator, Admin and Participant.
  - Creator: user who created the event, who can invite and set dives for admins and participants.
  - Admin: user invited by creator, who caan invite and set dives for participants.
  - Participant: user invited by admin/creator, who can start and end personal dives.
  
Event has a target (chosen/managed by creator/admin), a list of dives and has start + enddates

Targets are provided from [Kyppi](https://www.kyppi.fi/)

Inviting is done with messageObjects, which can be reused in future for other purposes.

Dives contain location, start+end and 'owner'.

Reset's are an object used for password resetting, with a 10 min expirytime.
