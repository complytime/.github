# ComplyTime: Cloud Native Compliance. Reimagined.

> From Code to Compliance, Intelligently.

ComplyTime is an engineering-first, API-driven framework designed to automate and unify compliance across the modern, cloud native landscape. We bridge the gap between high-level policy and technical implementation, empowering developers and securing your entire product portfolio.

## About ComplyTime

The world of compliance is at a crossroads. Traditional, document-centric models are failing to keep pace with the speed of cloud native development. ComplyTime was born from the need for a more agile, developer-focused solution. 

Our mission is to provide a unified, scanner-agnostic, and extensible microservice that transforms how organizations manage compliance artifacts. We believe in meeting developers where they are, integrating seamlessly into their workflows, and abstracting away the complexities of GRC (Governance, Risk, and Compliance) frameworks.

## Our Philosophy: Engineering-First

We believe that effective compliance automation must be built on a foundation that understands and respects developer workflows.

* **Engineering-Centric, Not Document-Centric**: Traditional compliance models digitize paperwork, resulting in massive, monolithic documents that hinder automation. ComplyTime adopts an engineering-first logical model, focusing on the granular, machine-readable data needed for true "compliance-as-code".
* **Built for Automation**: Our architecture is designed for the ephemeral, API-driven nature of cloud native systems. We enable programmatic, interactive engagement with compliance data, moving beyond slow, batch-processing of static files.
* **Flexible and Extensible**: A single standard cannot rule the modern compliance landscape. Reliance on a single standard creates unacceptable risk. ComplyTime is designed to be multi-standard and scanner-agnostic, ensuring long-term relevance and adaptability.

## Project Architecture

ComplyTime is built on a foundation of modern, microservice-based components designed for flexibility and scale.

* **[complyctl](./complyctl/)**: A CLI tool providing a consistent compliance foundation for platforms like RHEL.
* **[complyscribe](./complyscribe/)**: A key component of our pluggable framework, this service acts as a compliance-to-policy (C2P) engine, designed to be extensible for various compliance frameworks, not only OSCAL.
 <!-- TODO: A key component of our pluggable framework, this compliance authoring tool operates behind the scenes for an extensible integration for various compliance frameworks, not specific to OSCAL. -->
* **[complybeacon](./complybeacon/)**: A planned microservice for continuous compliance monitoring in distributed environments like OpenShift.
* **[complytime-demos](./complytime-demos/)**: A collection of demonstrations and examples for using the ComplyTime framework.

We leverage powerful, targeted open source components to achieve our goals. For instance, we utilize `oscal-sdk-go` and `compliance-to-policy-go`, sub-projects of OSCAL-Compass that align with our engineering-first, multi-standard vision.

## Community & Contributing

We are committed to the open source community. All of our governance, contribution guidelines, and community standards are located in our **[community repository](./community/)**.

* **[Governance](./community/GOVERNANCE.md)**: Our project roles and decision-making process.
* **[Contributing Guide](./community/CONTRIBUTING.md)**: How to get started with your first contribution.
* **[Code of Conduct](./community/CODE_OF_CONDUCT.md)**: Our community standards.

## The Road Ahead

Our vision is to establish ComplyTime as the definitive framework for modern, automated compliance. Our roadmap includes:

* **Deepening Cloud-Native Integration**: Enhancing our integration with core cloud-native technologies, including Red Hat Insights, Advanced Cluster Security (ACS), and OpenShift Observability.
* **Championing Open, Agile Standards**: Continuing to invest in and advocate for engineering-driven standards like Gemara that are purpose-built for the speed and scale of cloud-native development.

## Frequently Asked Questions (FAQ)

**Q: Does ComplyTime use OSCAL?**

A: Yes, but it is not limited to it. ComplyTime is a multi-standard platform. It leverages specific, targeted modules like `compliance-to-policy-go` to process OSCAL artifacts, but its architecture is designed to support a variety of formats, including Gemara, to avoid dependency on a single standard.

**Q: Why the focus on Gemara?**

A: Gemara represents an engineering-first approach to compliance automation, making it a natural fit for cloud-native workflows. Its backing by the OSSF and its role in the strategic OSPS Baseline initiative signal a major shift in the industry. Supporting Gemara allows us to address critical gaps left by document-centric standards and position ComplyTime at the forefront of modern compliance automation.

## Role-based Resources

**Relative association:**

* Cloud Native Developer / DevOps Engineer: see `DEVELOPERS.md`
* Security Professional / GRC Officer: see `COMPLIANCE_MANAGERS.md` and `AUDITORS.md`
* Open Source Contributors: see `DEVELOPERS.md`

## What You'll Need

* MacOS
* Linux machines
* Release downloads

### Useful commands

#### Getting the OSCAL Content

* Fork the  [`ComplianceAsCode/oscal-content`](https://github.com/ComplianceAsCode/oscal-content) repository.

* Clone the repository using `git clone git@github.com:ComplianceAsCode/oscal-content.git`. 

* Ensure that you run the command `git remote add upstream git@github.com:ComplianceAsCode/oscal-content.git` to ensure that your fork can easily stay up-to-date with the upstream. 



```bash
# Copying OSCAL Catalogs from oscal-content 
cp ~/{path-to-your-forked-oscal-content}/catalogs/ -r ~/.local/share/complytime/bundles/

# Copying OSCAL Profiles from oscal-content
cp ~/{path-to-your-forked-oscal-content}/profiles/ -r ~/.local/share/complytime/controls/

# Copying OSCAL Component Definitions from oscal-content
cp ~/{path-to-your-forked-oscal-content}/component-definitions/ -r ~/.local/share/complytime/controls/
```

The ~/.local/share/complytime/bundles and controls/ will hold the catalog.json, profile.json, and the component-definition.json that will allow for use with the complyctl commands.




```shell
make build
export COMPLYTIME_DEV_MODE=1
```

```bash
./bin/complyctl list # See the available frameworks
./bin/complyctl info <framework-id> 
./bin/complyctl plan <framework-id> --dry-run # See default assessment plan contents
./bin/complyctl plan <framework-id> --dry-run --out config.yml # Create a config file to edit assessment plan
./bin/complyctl plan <framework-id> --scope-config config.yml # Write assessment plan to workspace

```

#### Example OSCAL Content

[ANSSI catalog.json](https://github.com/ComplianceAsCode/oscal-content/blob/main/catalogs/anssi/catalog.json)

[RHEL10 ANSSI Minimal profile.json](https://github.com/ComplianceAsCode/oscal-content/blob/main/profiles/rhel10-anssi-minimal/profile.json)

![rhel10 anssi catalog](https://github.com/hbraswelrh/.github/blob/docs/profile-readme/profile/img/catalog.png?raw=true)

> Once the profile content has been copied to `~/.local/share/complytime/controls/profile.json` ensure the href is "file://controls/{name-of-catalog}.json"

![rhel10 anssi minimal profile](https://github.com/hbraswelrh/.github/blob/docs/profile-readme/profile/img/profile.png?raw=true)

[RHEL10 ANSSI Minimal component-definition.json](https://github.com/ComplianceAsCode/oscal-content/blob/main/component-definitions/rhel10/rhel10-anssi-minimal/component-definition.json)

![rhel10 anssi minimal component definition](https://github.com/hbraswelrh/.github/blob/docs/profile-readme/profile/img/compdef.png?raw=true)

> Once the component definition content has been copied to `~/.local/share/complytime/bundles/component-definition.json` the href should be the following: "file://controls/{name-of-profile}.json"

**`complyctl info --limit 5`**

![info](https://github.com/hbraswelrh/.github/blob/docs/profile-readme/profile/img/info.png?raw=true)

**`complyctl info --control r30 --limit 5`**

![info control](https://github.com/hbraswelrh/.github/blob/docs/profile-readme/profile/img/info-control.png?raw=true)

**`complyctl info --rule set_password_hashing_algorith_systemauth`**

![info rule](https://github.com/hbraswelrh/.github/blob/docs/profile-readme/profile/img/info-rule.png?raw=true)

**`complyctl info --parameter var_accounts_maximum_age_root`**

![info parameter](https://github.com/hbraswelrh/.github/blob/docs/profile-readme/profile/img/info-parameter.png?raw=true)
