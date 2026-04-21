
ATTACK 1 - POP PUBAT

ITS-S generates PriAT randomly
none knows PriAT (apart from the honest ITS-S)
ITS-S sends only one Auth request with PriAT
no replay attack of Auth request from ITS-S (implemented through a restriction)

=> The AA cannot issue two ATs with PubAT and different pseudoids: 

query attacker(PriAT) true
event(ValidATSent(pseudoid1, atverpk, authreq1)) 
&& event(VehicleAuthorizationRequestSent(authreq1)) (* The request should come from a hobest vehicle *)
&& event(ValidATSent(pseudoid2, atverpk, authreq2)) ==> pseudoid1 = pseudoid2.

Result: false (the attacker reads PubAT when the ITS-S uses AT and then asks for authorisation of PubAT, without knowing PriAT)

FIX1: version with PoP -> result: true
FIX2: AA has a list of already issued PubATs and does not issue the same PubAT two times
      Implemented with an axiom 
      result: true (even without PoP)



ATTACK 2 - REPLAY ATTACKS
Different models (see summary-auth-and-replay.png)

FIX1: see timestamps as sequence numbers
FIX2: see timestamps as time windows



ATTACK 3 - Compromised AA modifies attributes

event(ValidATReceived(enrcert, attributes)) ==> event(EAAuthorizingAT(enrcert, attributes)).

If an enrolled ITS-S (enrcert) has received a valid AT with attributes ==> the EA should have authorised those attributes for the ITS-S (enrcert)
Result: false (compromised AA issues the attributes and the AT without interacting with the EA)

FIX: signature of the EA on attributes in the auth response for the ITS-S -> result: true



ATTACK 4 - Compromised AA issues ATs

To honest ITS-S:
event(ValidATReceived(enrcert, reqea)) ==> event(EAAuthorizingAT(enrcert, reqea)).

If an enrolled ITS-S (enrcert) has received a valid AT intended to be authorised by the EA (recipient of reqea) ==> the the EA should have authorised the AT for the ITS-S (enrcert)
Result: false (compromised AA issues the AT without interacting with the EA)


To Attacker:
event(V2XMessageWithValidAT(m, at)) ==> HonestAAIssuingAT(at).

If an ITS-S receives a valid AT attached to a v2x message ==> A honest AA should have issued that AT as a result of the authorisation process
Result: false (the attacker, knowing PriAA, can issue the AT)



ATTACK 5: Compromised AA profiling the ITS-S based on the attributes it is requesting

The attacker knows some profiling_attributes
A process in which the ITS-S uses profiling attributes in the request with the AA should be indistinguishable from a process in which the ITS-S
uses non profiling attributes

Result observational equivalence: false (the attacker with PriAA can read the content of the auth request and check whether attributesreq == profiling attributes


ATTACK 6: Compromised AA issuing the same pseudoid in different ATs

event(ValidATReceivedWithV2XMessage(at1, pseudoid1)) && event(ValidATReceivedWithV2XMessage(at2, pseudoid2)) && at1 <> at2 
   ==> pseudoid1 <> pseudoid2.

If an ITS-S receives two different ats (at1 <> at2) ==> the ats should have different pseudoids
Result: false (the attacker, knowing PriAA, can create ats with the same pseudoid) 

Fix: pseudoid generated as hash of the PubAT -> result:true



ATTACK 7: ITS-S linkable based on the authority it interacts with

Two valid EAs
The attacker knows the certificates of both EAs

The attacker can distinguish which EA is contacted by the ITS-S

Result observational equivalence: false

Same for the AA










