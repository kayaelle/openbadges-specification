var specification=`

## Specification

### What is the problem this solves for?

The W3C Verifiable Credentials (VCs) are cryptographically verifiable claims that can be delivered as part of presentations that are also cryptographically verifiable. These layers of cryptographic proof can provide security and privacy enhancements to Open Badges that is not yet available in version 2.0. This can increase adoption by addressing market needs for trustworthy machine-ready data to power connected ecosystems in education and workforce. These enhancements have the added value of releasing issuers of the burden of hosting badge JSON and opening possibilities of using Open Badges to describe achievements with more personal detail. This proposal for a 3.0 version of Open Badges also includes adding achievementType to the BadgeClass, accompanying evidence with resultDescriptions, and considering how verifiable assertions can be used to describe single skill assessments.

__Verifiable Credentials Increase Trustworthiness of Open Badges__

Currently, Open Badges 2.0 data can be verified in two ways 1) publicly accessible hosted JSON badge data, 2) JWS digitally signed badges. Each of these methods is either less secure, less private, less trustworthy, or not flexible enough to meet the needs of the learners and third-party verifiers.

Publicly hosted badge data has been the preferred method of many Open Badges issuers. This method can risk the privacy of badge recipients who are reliant on the issuers to host their data leaving them with no control over its accessibility. There is also the potential that data about individuals is publicly accessible without their knowledge. Most Open Badges don't contain personally identifiable information to protect privacy but since most badge recipient profiles contain email addresses, if the emails are not hashed, they are publicly visible. This could lead to on-site identification, email spam, and also cause badges to be correlatable with other personally identifying data on the web.

Hosted badge data is also not tamper-evident since it is hosted on webservers typically as dynamically generated JSON files populated by queries made to relational databases or static JSON files. This makes the data easy to change without any historic reference or preservation. Changes to badge metadata such as criteria, the issuedOn date, and recipient email post verification can reduce the perceived quality of data and reflect wrong information about the learners' experiences.

Digitally signed 2.0 badges provide more security and privacy than the hosted badges. The verification process verifies the issuer and that the data has not been modified since it was signed. This method checks that there is a valid and accessible public key, that it is the correct signing key, the JWS verification passes, and the badge assertion is not found on a revocation list hosted by the issuer. This verification process reflects typical JWS signature suite methods, is the sole digital signature suite for Open Badges, and does not verify the recipients of badges.

For the most part, badges have been consumed by humans viewing attractive web pages hosted by issuers and/or shared online. This functionality won't disappear with 3.0 because badges on the web increase insights and exposure for issuers and learners. But web viewable badges are not machine verifiable and are not part of the Open Badges specification.

There's been very little evidence that badge JSON data is being readily consumed by machines, but technologies and the education and workforce markets have evolved since Open Badges 2.0 was released 4 years ago. Machine learning and AI uses have expanded alongside blockchain and other decentralized technologies creating opportunity for connecting learners to opportunities, more accurate skills-based hiring, and updated curriculums more equitably reflecting the needs of students. The market is demanding that the achievement data be trustworthy. This means that it should be accessible, protected, have integrity, and communicate what was intended including that the issuer and subjects of the data have been authenticated and that the data has not been tampered with since it was issued.

__Digital Wallets, Verifiable Presentations, and Learner Experiences__

Open Badges as VCs will be issued directly to learners who will accept the badges in their digital wallets which may be web, mobile, or desktop based (most are mobile right now). From the wallet, recipients can package their badges along with their other VCs, which could be education-related such as CLRs, government IDs, or other credentials, into verifiable presentations. A presentation contains the VCs that the learner wishes to share with a relying party. The digital wallet application digitally signs the presentation using the key of the learner. The verifying third-parties can cryptographically verify the presentation of the VCs as well as the VCs in the presentation without depending on the issuers.

Typically these verifiable presentations are sent in response to a request from a relying third-party. For example, a potential employer seeking to fill an internship role, may need to verify that a student is over 18, has completed a course on communication, and is a current student. A student could use their wallet to package three VCs (driver's license, course badge, and student ID) into a presentation that is signed by their private key. When the presentation is sent to the employer's website, the employer can verify that the VCs belong to the student and that the VCs are authentic.

A method used with VCs called Zero Knowledge Proof (ZKP) increases privacy capability while not detracting from the value of the VCs or their authenticity. The student can respond to the employer by creating a verifiable presentation that can verify age, contain a grade for the communications course, and a student status without revealing other private information typically in the mentioned credentials such as their date of birth, address, photo, or even the name of the school they attend. This maintains privacy for the student and provides the verifiable data the employer needs. It is improper for Open Badges to publicly host a JSON file that contains grading information or other PII. A VC Open Badge could contain grades and PII because the claim is made privately by the issuer to the learner. It is then up to learner to decide the visibility of this information. This could potentially allay FERPA issues and allow for richer metadata.

####ADD SOMETHING ABOUT DIDs & VERIFIABLE REGIStIRES/TRUST TRIANGLE HERE?####

__Can depend on VC ecosystem for cryptographic signature suites and other VC functionality__

Verifiable credentials and presentations can be used for any type of claim. Members of the community include security and cryptography experts who are issuing verifiable credentials about health records such as vaccination passports, shipping containers, government IDs, as well as education and occupational credentials. This allows IMS to use best of breed solutions that arise from the VC ecosystem and focus on the needs of the education ecosystem.

 __Solve a long-standing issue in Open Badges: creators of badges are not always the Issuers__

Verifiable Credential place issuer profile information at the assertion level rather than the claim level to align with the cryptographic proof methods. This creates the potential to add a creator property to the BadgeClass. This could also include a property that defines the relationship between the creator and the issuer to provide deeper understanding to relying third-parties.

KL: EXPAND

 __Open Badges are more than micro-credentials__

The CLR contains a property, achievementType, that when included in the BadgeClass will explain the context of an Open Badge and clarify the misunderstanding that all Open Badges are micro-credentials. This will increase the perceived significance and usage of Open Badges to deliver single achievements such as degrees, licenses, courses, etc.

KL: USE CASE EXAMPLES

__Result Descriptions__

NATE, can you please describe?

__Skill Assertions__

NATE, can you please describe?


### Changes to the data model

####Changes to Assertion

Verifiable Credentials have properties to describe an assertion of a claim and the instructions for cryptographic proof of the claim. As seen in the examples below, these properties will replace the assertion Object as it has been used in 2.0. For example, issuanceDate will be replaced by issuedOn, expires by expirationDate, verification by proof.

Issuer will move from the badgeclass to the VC assertion. Recipient will move into the credentialSubject ID property. Badge will no longer be called in the assertion but be described in the credentialSubject hasCredential property. [Evidence](https://www.w3.org/TR/vc-data-model/#evidence) in Verifiable Credentials supports the cryptographic integrity/proof of the verifiable credential. Evidence of Achievement should be associated with the credentialSubject.id (learner). ResultDescriptions may also be added...

Baked badge images will no longer be required (are they required now?)

Additions to the BadgeClass include AchievementType. Badge images can be optional. With Verifiable Credentials images aren't required although some issuers and wallets may find them just as useful as they were in 2.0


KL - discuss Verifiable Skills - Reference:  Nate's Lucid Chart.


KL: Add table of properties


### Changes to the Validator

(Let folks know I added this section because it seems critical)

This proposal will incur modifications to the validator and considerations as to how the validator handles prior versions of Open Badges and VC Open Badges. The working group can discuss topics such as whether validators should remain separate and if validated VC Open Badges should return VCs as receipts upon validation.

KL: expand

### Changes to the API

As with the validator, the BadgeConnect API will require adjustments to accommodate property changes.

KL: EXPAND

### Considerations

<aside class="note">Platforms that adopt this will still be able to display Open Badges as HTML. Issuers will need to adopt cryptographic signature strategies as recommended by the VC community.</aside>

KL: Add to this

### Examples

<figure class="example">
  <pre>
    {

    }
  </pre>
  <figcaption><span>Example of Open Badge as a Verifiable Credential</span></figcaption>
</figure>

<figure class="example">
  <pre>
    {

    }
  </pre>
  <figcaption><span>Example of Open Badge as a Verifiable Credential in a Verifiable Presentation</span></figcaption>
</figure>

<figure class="example">
  <pre>
    {

    }
  </pre>
  <figcaption><span>Example of Two Open Badges as Verifiable Credentials in a Verifiable Presentation</span></figcaption>
</figure>

<figure class="example">
  <pre>
    {

    }
  </pre>
  <figcaption><span>Example of skill assertion</span></figcaption>
</figure>


### Example Admonitions

KL/NATE: (Do we need this?)

<aside class="note">Example of text content of note aside</aside>
<aside class="warning">Example of text content of warning aside</aside>
<aside class="issue">Example of text content of issue aside</aside>


`;
