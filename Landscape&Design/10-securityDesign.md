# Security

**Security is designed into Google’s technical infrastructure**.

|Layer | Notable security measures (among others)|
|---|---|
|Operational security | Intrusion detection systems; techniques to reduce insider risk; employee U2F use; software development practices|
|Internet communication | Google Front End; designed-in Denial of Service protection|
|Storage services | Encryption at rest|
|User identity | Central identity service with support for U2F|
|Service deployment | Encryption of inter-service communication|
|Hardware infrastructure | Hardware design and provenance; secure boot stack; premises security|


Hardware design and provenance: Both the server boards and the networking
equipment in Google data centers are custom-designed by Google. Google also
designs custom chips, including a hardware security chip that is currently being
deployed on both servers and peripherals.
Secure boot stack: Google server machines use a variety of technologies to ensure
that they are booting the correct software stack, such as cryptographic signatures
over the BIOS, bootloader, kernel, and base operating system image.
Premises security: Google designs and builds its own data centers, which incorporate
multiple layers of physical security protections. Access to these data centers is limited
to only a very small fraction of Google employees. Google additionally hosts some
servers in third-party data centers, where we ensure that there are Google-controlled
physical security measures on top of the security layers provided by the data center
operator.
Encryption of inter-service communication: Google’s infrastructure provides
cryptographic privacy and integrity for remote procedure call (“RPC”) data on the
network. Google’s services communicate with each other using RPC calls. The
infrastructure automatically encrypts all infrastructure RPC traffic which goes between
data centers. Google has started to deploy hardware cryptographic accelerators that
will allow it to extend this default encryption to all infrastructure RPC traffic inside
Google data centers.
User identity: Google’s central identity service, which usually manifests to end users
as the Google login page, goes beyond asking for a simple username and password.
The service also intelligently challenges users for additional information based on risk
factors such as whether they have logged in from the same device or a similar
location in the past. Users also have the option of employing second factors when
signing in, including devices based on the Universal 2nd Factor (U2F) open standard
Encryption at rest: Most applications at Google access physical storage indirectly via
storage services, and encryption (using centrally managed keys) is applied at the
layer of these storage services. Google also enables hardware encryption support in
hard drives and SSDs.
Google Front End (“GFE”): Google services that want to make themselves available
on the Internet register themselves with an infrastructure service called the Google
Front End, which ensures that all TLS connections are terminated using correct
certificates and following best practices such as supporting perfect forward secrecy.
The GFE additionally applies protections against Denial of Service attacks.
Denial of Service (“DoS”) protection: The sheer scale of its infrastructure enables
Google to simply absorb many DoS attacks. Google also has multi-tier, multi-layer
DoS protections that further reduce the risk of any DoS impact on a service running
behind a GFE.
Intrusion detection: Rules and machine intelligence give operational security
engineers warnings of possible incidents. Google conducts Red Team exercises to
measure and improve the effectiveness of its detection and response mechanisms.
Reducing insider risk: Google aggressively limits and actively monitors the activities of
employees who have been granted administrative access to the infrastructure.
Employee U2F use: To guard against phishing attacks against Google employees,
employee accounts require use of U2F-compatible Security Keys.
Software development practices: Google employs central source control and requires
two-party review of new code. Google also provides its developers libraries that
prevent them from introducing certain classes of security bugs. Google also runs a
Vulnerability Rewards Program where we pay anyone who is able to discover and
inform us of bugs in our infrastructure or applications.