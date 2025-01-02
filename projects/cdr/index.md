# CDR BLOG POST

Content Disarm and Reconstruction (CDR) is a technology that removes potentially malicious threats from files. A common place application of CDR tools is scanning incoming email attachments, such as Microsoft Office documents or PDFs, for malware. The tool may deconstruct and analyze the file, remove parts of the file deemed suspicious, and then reconstruct the file with the remaining pieces. This process ensures that only safe and sanitized content reaches the end-user, significantly reducing the risk of malware infections. CDR technology is also an integral part of Cross-Domain Solutions (CDS), integrated software-hardware systems that facilitate the access or transfer of information between multiple security domains that may have different security classifications or policies. Today, CDS systems are widely used in military and intelligence environments, and the importance of secure, effective CDS remains high with the introduction of the NSA's "Raising the Bar" (RTB) initiative. This initiative underscores the critical need for robust security measures in environments where sensitive information is frequently exchanged.

The D3FEND team has started modeling components of the Content Disarm and Reconstruction pipeline. This blog post will detail the methodology and reasoning we used and depict our resulting model with D3FEND's CAD tool. By doing so, we aim to provide a comprehensive framework that can be utilized by cybersecurity professionals to enhance their understanding and implementation of CDR techniques.


## A Brief Introduction to CAD

CADUCEUS (Cyber Attack-Defense Utility for Capturing Engagements and Understandable Scenarios), or CAD for short, is a new tool being developed by the D3FEND team to support modeling and graphing use cases. The tool lets you easily drag and drop nodes to represent ATT&CK and D3FEND techniques, digital artifacts, and more, which can be populated with a specific class such as d3f:WebApplicationFirewall. Additionally, edges can be drawn between nodes to represent relationships between classes, and the options are prepopulated with relationships currently defined in D3FEND.  CAD harnesses the power of the D3FEND ontology to perform automated reasoning on certain types of nodes. For example, from a single digital artifact node, users can then see what offensive and defensive techniques are related to that node, as well as the full set of class inferences for that digital artifact, and vice versa. This feature allows users to explore complex relationships and dependencies within cybersecurity scenarios, offering deeper insights into potential vulnerabilities and mitigation strategies. We hope that this tool can be used to aid the visual representation of a wide array of use cases, with different levels of granularity, from modeling a full adversary campaign to a malware sample. For more information, check out d3fend.mitre.org/cad and click help for documentation.

## Methodology

Like the rest of the content within D3FEND, we utilized numerous sources of research and patent literature to gather information about specific techniques utilized in CDR technology at a detailed technical level. While doing so, we kept techniques that were cybersecurity-related and excluded those that were not, such as physical techniques. We then abstracted techniques into a Content Filtering (d3f:ContentFiltering) taxonomy before diving into defining digital artifacts associated with the techniques. While the existing D3FEND ontology had some relevant digital artifacts, this work required additional artifacts to be added to the ontology. Finally, we defined precise relationships between the artifacts themselves and the techniques. As a result, we have added X new techniques and Y new digital artifacts to the D3FEND framework.

#### Challenges

While there are countless vendors offering CDR and CDS products, due to the confidential nature of its applications and the competitive vendor landscape, it was quite challenging to research what specific CDR techniques the products use. The information available on vendor websites is vague and there aren't many patents in this space, likely because vendors want to keep their propriety knowledge confidential. While the NSA has created the RTB initiative in 2018, which has continuously set guidelines including security standards and requirements to secure CDS systems, the details aren't publicly accessible. In summary, open-source knowledge on CDR is neither in-depth nor easily accessible, but that is a problem this work attempts to solve. 

## Deconstructing CDR

Content Disarm and Reconstruction (CDR) is not listed as a D3FEND technique as it is composite; that is, it is composed of a series of techniques in a pipeline:​

- verification​
- content extraction & inspection​
- sanitization​
- augmentation​
- reconstruction

Among these discrete steps outlined above, some steps are not specifically security related. Specifically, a CDR tool may deconstruct and then reconstruct content regardless of it being infected or not. Additionally, the atomic steps of deconstruction and reconstruction does not inherently improve the security of the content in a useful way. Thus, we have focused on the intermediate filtering step that encompasses validating and altering the content so that the output after the entire CDR process is a sanitized version. The key is that all sub-techniques of Content Filtering (d3f:ContentFiltering) focus on ensuring compliance of a specific security-focused Content Policy (d3f:ContentPolicy).  Content Filtering is separated into three sub-techniques: Content Validation (d3f:ContentValidation) checks if the content adheres to the security policy, Content Transformation (d3f:ContentTransformation) modifies the content to a state of compliance, whether by removing, replacing, or converting, and then finally, there is an option to quarantine non-compliant content. This structured approach allows for flexibility and adaptability in handling diverse content types and security requirements.

## File Format Verification Deep Dive

<!-- Embed the HTML iframe below -->
<!DOCTYPE html>

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>D3FEND EMBEDDED</title>

    <script>
      const user_data = {
  "nodes": [
    {
      "id": "0.7032304012631014",
      "type": "countermeasure-node",
      "position": {
        "x": -501.33698767238593,
        "y": 106.91303071623031
      },
      "data": {
        "label": " Content Filtering",
        "sequence": "0",
        "user_properties": [],
        "d3f_class": ":ContentFiltering",
        "d3f_class_label": " Content Filtering"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 444,
        "height": 235
      },
      "selected": false,
      "dragging": false,
      "width": 444,
      "height": 235
    },
    {
      "id": "0.47249815289283914",
      "type": "countermeasure-node",
      "position": {
        "x": 78.29788411488562,
        "y": -354.7431600138998
      },
      "data": {
        "label": "Content Validation",
        "sequence": "0",
        "user_properties": [
          [
            "d3f:definition",
            "Verify and validate contents complies with policy"
          ],
          [
            "reference",
            "https://patentimages.storage.googleapis.com/ba/10/83/968a6345eee505/US20200104494A1.pdf"
          ]
        ],
        "d3f_class": ":ContentValidation",
        "d3f_class_label": "Content Validation"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 177
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "9-copy0.9142249922179582",
      "type": "countermeasure-node",
      "position": {
        "x": 29.3199608035639,
        "y": 127.62360787653802
      },
      "data": {
        "label": "Content Tranformation",
        "sequence": "0",
        "user_properties": [
          [
            "d3f:definition",
            "Modify content that does not comply with policy"
          ],
          [
            "reference",
            "https://patentimages.storage.googleapis.com/a9/40/78/713c8deb2c4c7a/US20190268352A1.pdf"
          ]
        ],
        "d3f_class": ":ContentTranformation",
        "d3f_class_label": "Content Tranformation"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 138
      },
      "selected": false,
      "dragging": false,
      "width": 409,
      "height": 138
    },
    {
      "id": "0.48426736445356067",
      "type": "countermeasure-node",
      "position": {
        "x": 12.846699712515232,
        "y": 609.4157038334808
      },
      "data": {
        "label": "Content Quarantine",
        "sequence": "0",
        "user_properties": [
          [
            "d3f:definition",
            "Transfer content that does not comply with policy to quanrantine zone"
          ],
          [
            "reference",
            "https://patentimages.storage.googleapis.com/a9/40/78/713c8deb2c4c7a/US20190268352A1.pdf"
          ]
        ],
        "d3f_class": ":ContentQuarantine",
        "d3f_class_label": "Content Quarantine"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 177
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.5762349378605824",
      "type": "countermeasure-node",
      "position": {
        "x": 643.4234401020959,
        "y": 364.446353177799
      },
      "data": {
        "label": "Content Format Conversion",
        "sequence": "0",
        "user_properties": [
          [
            "d3f:definition",
            "Converting a file from one form to another, usually a simpler and safer format"
          ],
          [
            "reference",
            "https://patentimages.storage.googleapis.com/a9/40/78/713c8deb2c4c7a/US20190268352A1.pdf"
          ]
        ],
        "d3f_class": ":ContentFormatConversion",
        "d3f_class_label": "Content Format Conversion"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 177
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.7617608511325669",
      "type": "countermeasure-node",
      "position": {
        "x": 644.6621833695679,
        "y": -76.4266741579388
      },
      "data": {
        "label": "Content Excision",
        "sequence": "0",
        "user_properties": [
          [
            "d3f:definition",
            "Removing specific, potentially malicious, parts of content"
          ],
          [
            "reference",
            "https://patentimages.storage.googleapis.com/a9/40/78/713c8deb2c4c7a/US20190268352A1.pdf"
          ]
        ],
        "d3f_class": ":ContentExcision",
        "d3f_class_label": "Content Excision"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 177
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.0744514779826817",
      "type": "countermeasure-node",
      "position": {
        "x": 645.0438615464395,
        "y": 141.42270556041683
      },
      "data": {
        "label": "Content Substitution",
        "sequence": "0",
        "user_properties": [
          [
            "d3f:definition",
            "Replace specific parts of content with something else"
          ],
          [
            "reference",
            "https://patentimages.storage.googleapis.com/a9/40/78/713c8deb2c4c7a/US20190268352A1.pdf"
          ]
        ],
        "d3f_class": ":ContentSubstitution",
        "d3f_class_label": "Content Substitution"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 177
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.5507247954821324",
      "type": "artifact-node",
      "position": {
        "x": 2738.2911589668497,
        "y": 158.66995602974254
      },
      "data": {
        "label": "File Section",
        "sequence": "0",
        "user_properties": [],
        "d3f_class": "d3f:FileSection",
        "d3f_class_label": "File Section"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 356,
        "height": 148
      },
      "selected": false,
      "dragging": false,
      "width": 356,
      "height": 148
    },
    {
      "id": "0.28963955228702054",
      "type": "artifact-node",
      "position": {
        "x": 4446.058026557275,
        "y": -85.0223968519312
      },
      "data": {
        "label": "File Magic Bytes",
        "sequence": "0",
        "user_properties": [
          [
            "definition",
            "A specific type of header signature located at the beginning of a file, used to identify the file format."
          ]
        ],
        "d3f_class": ":FileMagicBytes",
        "d3f_class_label": "File Magic Bytes"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 107
      },
      "selected": false,
      "dragging": false,
      "width": 207,
      "height": 107
    },
    {
      "id": "0.0490499135274598",
      "type": "artifact-node",
      "position": {
        "x": 3303.949438561061,
        "y": -184.19381463278728
      },
      "data": {
        "label": "File Header Block",
        "sequence": "0",
        "user_properties": [
          [
            "definition",
            "Headers are sections of a file that organize and provide information about specific sections or components of the file. Typically found at the beginning of a file, they often contain file type identification, version information, and metadata such as size, format, and encoding."
          ]
        ],
        "d3f_class": ":FileHeaderBlock",
        "d3f_class_label": "File Header Block"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 102
      },
      "selected": false,
      "dragging": false,
      "width": 309,
      "height": 102
    },
    {
      "id": "0.1230247439051928",
      "type": "artifact-node",
      "position": {
        "x": 3297.6336863032166,
        "y": 161.6435723258549
      },
      "data": {
        "label": "File Content Block",
        "sequence": "0",
        "user_properties": [
          [
            "definition",
            "A section within a file that contains the main content or data payload."
          ]
        ],
        "d3f_class": ":FileContentBlock",
        "d3f_class_label": "File Content Block"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 134
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "-copy0.23195137482463135",
      "type": "artifact-node",
      "position": {
        "x": 1796.338245642954,
        "y": 1261.7692614436212
      },
      "data": {
        "label": "File Metadata",
        "sequence": "0",
        "user_properties": [
          [
            "definition",
            "Information that describes and provides context about a file's content, structure, and attributes."
          ]
        ],
        "d3f_class": ":FileMetadata",
        "d3f_class_label": "File Metadata"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 148
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.34302096991368103",
      "type": "artifact-node",
      "position": {
        "x": 3907.8163768423506,
        "y": -294.5020661272177
      },
      "data": {
        "label": "File Header Block Content",
        "sequence": "0",
        "user_properties": [
          [
            "definition",
            "The content of a header block not including the signature."
          ]
        ],
        "d3f_class": ":FileHeaderBlockContent",
        "d3f_class_label": "File Header Block Content"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 134
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.09325736548375141",
      "type": "artifact-node",
      "position": {
        "x": 3918.0563337197877,
        "y": 255.08403653645013
      },
      "data": {
        "label": "File Content Block Metadata",
        "sequence": "0",
        "user_properties": [
          [
            "definition",
            "Content Blocks may contain metadata specific to the block's content at the beginning"
          ]
        ],
        "d3f_class": ":FileContentBlockMetadata",
        "d3f_class_label": "File Content Block Metadata"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 134
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.30470669924201865",
      "type": "artifact-node",
      "position": {
        "x": 3911.9430224696885,
        "y": 87.88827897265487
      },
      "data": {
        "label": "File Content Block Data",
        "sequence": "0",
        "user_properties": [
          [
            "definition",
            "The actual content or main data within a file or data block."
          ]
        ],
        "d3f_class": ":FileContentBlockData",
        "d3f_class_label": "File Content Block Data"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 134
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.40552351868555836",
      "type": "countermeasure-node",
      "position": {
        "x": 652.9725993341016,
        "y": -355.0182774021778
      },
      "data": {
        "label": "File Format Verification",
        "sequence": "0",
        "user_properties": [
          [
            "d3f:definition",
            "verifying that a file conforms to its expected format specifications"
          ],
          [
            "reference",
            "https://patentimages.storage.googleapis.com/ba/10/83/968a6345eee505/US20200104494A1.pdf"
          ]
        ],
        "d3f_class": ":FileFormatVerification",
        "d3f_class_label": "File Format Verification"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 177
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.6146071780317519",
      "type": "artifact-node",
      "position": {
        "x": 2278.62500967582,
        "y": 161.1446608108434
      },
      "data": {
        "label": "File",
        "sequence": "0",
        "user_properties": [],
        "d3f_class": "d3f:File",
        "d3f_class_label": "File"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 241,
        "height": 113
      },
      "selected": false,
      "dragging": false,
      "width": 241,
      "height": 113
    },
    {
      "id": "0.7314564313202583",
      "type": "artifact-node",
      "position": {
        "x": 1796.273377670382,
        "y": 801.3286046642634
      },
      "data": {
        "label": "Content Policy",
        "sequence": "0",
        "user_properties": [
          [
            "definition",
            "A set of rules and guidelines that dictate the acceptable use, distribution, and management of digital content within a system or platform. It defines what content is allowed, restricted, or prohibited, ensuring compliance with legal, ethical, and organizational standards."
          ]
        ],
        "d3f_class": ":ContentPolicy",
        "d3f_class_label": "Content Policy"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 190
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.7752203564382074",
      "type": "note-node",
      "position": {
        "x": 3286.4618550418118,
        "y": 1020.6772720465565
      },
      "data": {
        "label": "",
        "sequence": "0",
        "user_properties": [
          [
            "rdfs:comment",
            "Includes Enclosed Docs, Scripts, Macros, Images, Video, Embedded Obj, Hyperlink, forms"
          ]
        ]
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 493,
        "height": 75
      },
      "selected": false,
      "dragging": false,
      "width": 454,
      "height": 75
    },
    {
      "id": "0.1189036182761879",
      "type": "artifact-node",
      "position": {
        "x": 2439.862157690674,
        "y": 1010.5424658850889
      },
      "data": {
        "label": "Structured Digital Information Content",
        "sequence": "0",
        "user_properties": [],
        "d3f_class": ":StructuredDigitalInformationContent",
        "d3f_class_label": "Structured Digital Information Content"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 302,
        "height": 99
      },
      "selected": false,
      "dragging": false,
      "width": 302,
      "height": 99
    },
    {
      "id": "0.34945809922391347",
      "type": "countermeasure-node",
      "position": {
        "x": 1394.2575113083624,
        "y": -1001.6322379996101
      },
      "data": {
        "label": "Header And Footer Verification",
        "sequence": "0",
        "user_properties": [
          [
            "d3f:definition",
            "Utilizing the static Header and Footer sections to validate the file"
          ],
          [
            "reference",
            "https://core.ac.uk/download/pdf/326762883.pdf"
          ],
          [
            "reference",
            "https://www.sciencedirect.com/science/article/pii/S1742287607000369?viewFullText=true#sec4"
          ]
        ],
        "d3f_class": ":HeaderAndFooterVerification",
        "d3f_class_label": "Header And Footer Verification"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 195
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.3258831965382004",
      "type": "countermeasure-node",
      "position": {
        "x": 2003.690577432811,
        "y": -1003.6951116516527
      },
      "data": {
        "label": "File Magic Byte Verification",
        "sequence": "0",
        "user_properties": [
          [
            "d3f:definition",
            "Utilizing the magic number to verify the file"
          ],
          [
            "reference",
            "https://pure.uva.nl/ws/files/1739225/132135_thesis.pdf"
          ],
          [
            "reference",
            "https://www.sciencedirect.com/science/article/pii/S1742287607000369?viewFullText=true#sec4"
          ]
        ],
        "d3f_class": ":FileMagicByteVerification",
        "d3f_class_label": "File Magic Byte Verification"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 195
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.9774559813293479",
      "type": "countermeasure-node",
      "position": {
        "x": 1395.5543829749845,
        "y": -723.8417969444534
      },
      "data": {
        "label": "Container Structure Validation",
        "sequence": "0",
        "user_properties": [
          [
            "d3f:definition",
            "Container Structure Validation verifies the integrity and correctness of files that contain multiple internal sections or data structures by checking the consistency of integers, pointers, and other structural elements within a file to ensure they adhere to predefined specifications."
          ],
          [
            "reference",
            "https://www.sciencedirect.com/science/article/pii/S1742287607000369?viewFullText=true#sec4"
          ],
          [
            "reference",
            "https://pure.uva.nl/ws/files/1739225/132135_thesis.pdf"
          ]
        ],
        "d3f_class": ":ContainerStructureValidation",
        "d3f_class_label": "Container Structure Validation"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 265
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.2756682259786878",
      "type": "countermeasure-node",
      "position": {
        "x": 1396.5733547161838,
        "y": -370.0841755616352
      },
      "data": {
        "label": "File Content Decompression Checking",
        "sequence": "0",
        "user_properties": [
          [
            "d3f:definition",
            "Checking if compressed or encoded data sections can be successfully decompressed or decoded. Can follow with further analysis with semantic knowledge"
          ],
          [
            "reference",
            "https://www.sciencedirect.com/science/article/pii/S1742287607000369?viewFullText=true#sec4"
          ],
          [
            "reference",
            "https://pure.uva.nl/ws/files/1739225/132135_thesis.pdf"
          ]
        ],
        "d3f_class": ":FileContentDecompressionChecking",
        "d3f_class_label": "File Content Decompression Checking"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 237
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.36833599672722817",
      "type": "countermeasure-node",
      "position": {
        "x": 1406.0765711764095,
        "y": 177.7472065917516
      },
      "data": {
        "label": "Algorithm Output Analysis",
        "sequence": "0",
        "user_properties": [
          [
            "d3f:definition",
            "Determine whether a block of data was compressed/encoded in a specific way by using bit sequence matching"
          ],
          [
            "reference",
            "https://pure.uva.nl/ws/files/1739225/132135_thesis.pdf"
          ],
          [
            "kb-article",
            " For example, JPEG uses Huffman coding to compress data. Given a block of data, it is possible to determine whether it was likely compressed with a given Huffman table using bit sequence matching "
          ]
        ],
        "d3f_class": ":AlgorithmOutputAnalysis",
        "d3f_class_label": "Algorithm Output Analysis"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 265
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.16229972296000217",
      "type": "countermeasure-node",
      "position": {
        "x": 1405.9979754731005,
        "y": -74.84267647495558
      },
      "data": {
        "label": "Internal Verification Checking",
        "sequence": "0",
        "user_properties": [
          [
            "d3f:definition",
            "Utilizes actual contents of a file to verify file format (verifying data using CRCs)"
          ],
          [
            "reference",
            "https://pure.uva.nl/ws/files/1739225/132135_thesis.pdf"
          ]
        ],
        "d3f_class": ":InternalVerificationChecking",
        "d3f_class_label": "Internal Verification Checking"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 177
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.9514174898243452",
      "type": "countermeasure-node",
      "position": {
        "x": 1396.4110012186093,
        "y": -1229.9351896808016
      },
      "data": {
        "label": "File Entropy Anomaly Detection",
        "sequence": "0",
        "user_properties": [
          [
            "d3f:definition",
            "Utilizing entropy values as a signature to identify different file types"
          ],
          [
            "reference",
            "https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=4732193"
          ]
        ],
        "d3f_class": ":FileEntropyAnomalyDetection",
        "d3f_class_label": "File Entropy Anomaly Detection"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 177
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.20366737316992256",
      "type": "artifact-node",
      "position": {
        "x": 1787.19308955642,
        "y": 1500.8255290918723
      },
      "data": {
        "label": "Metadata",
        "sequence": "0",
        "user_properties": [],
        "d3f_class": "d3f:Metadata",
        "d3f_class_label": "Metadata"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 150,
        "height": 102
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.9672516677158717",
      "type": "artifact-node",
      "position": {
        "x": 3912.541234948633,
        "y": -111.2971259445954
      },
      "data": {
        "label": "File Header Signature",
        "sequence": "0",
        "user_properties": [
          [
            "definition",
            "A sequence of bytes used to identify and validate specific header sections within a file."
          ]
        ],
        "d3f_class": ":FileHeaderSignature",
        "d3f_class_label": "File Header Signature"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 134
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.14499280157174388",
      "type": "artifact-node",
      "position": {
        "x": 3294.0413515291857,
        "y": 541.1733411878436
      },
      "data": {
        "label": "File Footer Block",
        "sequence": "0",
        "user_properties": [
          [
            "definition",
            "A section at the end of a file that contains metadata or control information."
          ]
        ],
        "d3f_class": ":FileFooterBlock",
        "d3f_class_label": "File Footer Block"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 134
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.16090754731449974",
      "type": "artifact-node",
      "position": {
        "x": 2444.0085424312115,
        "y": 1263.4847553526417
      },
      "data": {
        "label": "Digital Information",
        "sequence": "0",
        "user_properties": [],
        "d3f_class": "d3f:DigitalInformation",
        "d3f_class_label": "Digital Information"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 150,
        "height": 102
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.270595913540307",
      "type": "artifact-node",
      "position": {
        "x": 3898.628014033057,
        "y": 684.4599586502709
      },
      "data": {
        "label": "File Footer Block Content",
        "sequence": "0",
        "user_properties": [
          [
            "definition",
            "The content of a footer block not including the signature."
          ]
        ],
        "d3f_class": ":FileFooterBlockContent",
        "d3f_class_label": "File Footer Block Content"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 134
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.8253744550116549",
      "type": "note-node",
      "position": {
        "x": 4592.607395726958,
        "y": 1251.2552701335933
      },
      "data": {
        "label": "ZIP FILE",
        "sequence": "0",
        "user_properties": [
          [
            "rdfs:comment",
            "Example zip file\n\n1. Local File Header A.txt\n2. Data for A.txt\n3. Local File Header B.txt\n4. Data for B.txt\n5. Central Directory Header A.txt\n6. Central Directory Header B.txt\n7. End of central directory record\n\n\n\n\n1. Header Block\n        header signature: 0x504b0304\n2. Content Block\n3. Header Block\n        header signature: 0x504b0304\n4. Content Block\n5. Header Block\n        header signature: 0x504b0102\n6. Header Block\n        header signature: 0x504b0102\n\n7. Footer Block\n       footer signature: 0x503b0506\n"
          ]
        ]
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 242,
        "height": 541
      },
      "selected": false,
      "dragging": false,
      "width": 242,
      "height": 541
    },
    {
      "id": "0.6136178162729569",
      "type": "artifact-node",
      "position": {
        "x": 3907.1174509129846,
        "y": 493.76922414518896
      },
      "data": {
        "label": "File Footer Signature",
        "sequence": "0",
        "user_properties": [
          [
            "definition",
            "A sequence of bytes used to identify and validate the footer section within a file."
          ]
        ],
        "d3f_class": ":FileFooterSignature",
        "d3f_class_label": "File Footer Signature"
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 462,
        "height": 134
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.8199907918822567",
      "type": "note-node",
      "position": {
        "x": 4891.871454331573,
        "y": 1254.1370835834248
      },
      "data": {
        "label": "PDF FILE",
        "sequence": "0",
        "user_properties": [
          [
            "rdfs:comment",
            "Example PDF file\n\n\n1. Header\n2. Body\n3. Cross Reference Table\n4. Trailer\n\n\n\n\n1. Header Block\n         header signature: %PDF-1.7\n2. Content Block\n3. Header Block\n          header signature: xref\n4. Footer Block\n          footer signature: trailer\n"
          ]
        ]
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 194,
        "height": 313
      },
      "selected": false,
      "dragging": false
    },
    {
      "id": "0.15630497336477822",
      "type": "note-node",
      "position": {
        "x": 5162.339067020135,
        "y": 1255.4976247141924
      },
      "data": {
        "label": "PE32",
        "sequence": "0",
        "user_properties": [
          [
            "rdfs:comment",
            "Example PE file\n\n\n1. DOS Header\n2. DOS stub\n3. NTHeaders\n4. Section Table\n5. Sections (.text, .rdata, etc)\n\n\n1. Header Block\n2. Content Block\n3. Header Block\n4. Header Block\n5. Content Block\n\n\n"
          ]
        ]
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 219,
        "height": 273
      },
      "selected": false,
      "width": 219,
      "height": 273,
      "dragging": false
    },
    {
      "id": "0.5764862604479757",
      "type": "note-node",
      "position": {
        "x": 4097.568046120161,
        "y": 1252.709566784229
      },
      "data": {
        "label": "libmagic",
        "sequence": "0",
        "user_properties": [
          [
            "rdfs:comment",
            "Libmagic has a custom domain specific language (DSL) for specifying file patterns\n\n- Located in /usr/local/share/misc/magic\n\n\nExample:\n\n10        lelong    0x00000100    this is a test\n>20       ubyte 0xFF       test two\n!:mime    application/x-foo\n\n\n1. Start at byte offset 10, read singed little-endian long, if equal to 0x100, print \"this is a test\"\n2. If test 1 is true, test if byte offset 20 equals 0xFF, print \"test two\", and associate file with MIME type application/x-foo\n\n\n\n"
          ]
        ]
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 640,
        "height": 253
      },
      "selected": false,
      "width": 640,
      "height": 253,
      "dragging": false
    },
    {
      "id": "0.1608709589078562",
      "type": "note-node",
      "position": {
        "x": 3971.397819321481,
        "y": 1541.0281689718718
      },
      "data": {
        "label": "TrID",
        "sequence": "0",
        "user_properties": [
          [
            "rdfs:comment",
            "TrID has a database of XML files containing rules/patterns to match...\n\n\nUnable to see what the XML files themselves\n"
          ]
        ]
      },
      "origin": [
        0.5,
        0
      ],
      "measured": {
        "width": 379,
        "height": 117
      },
      "selected": false,
      "dragging": false
    }
  ],
  "edges": [
    {
      "type": "editableEdge",
      "data": {
        "label": "d3f:may-contain",
        "d3f_property": "d3f:may-contain"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.0490499135274598",
      "sourceHandle": "source",
      "target": "0.34302096991368103",
      "targetHandle": "target",
      "id": "xy-edge__0.0490499135274598source-0.34302096991368103target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "d3f:may-contain",
        "d3f_property": "d3f:may-contain"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.1230247439051928",
      "sourceHandle": "source",
      "target": "0.09325736548375141",
      "targetHandle": "target",
      "id": "xy-edge__0.1230247439051928source-0.09325736548375141target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "contains",
        "d3f_property": "contains"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.1230247439051928",
      "sourceHandle": "source",
      "target": "0.30470669924201865",
      "targetHandle": "target",
      "id": "xy-edge__0.1230247439051928source-0.30470669924201865target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "contains",
        "d3f_property": "d3f:contains"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.6146071780317519",
      "sourceHandle": "source",
      "target": "0.5507247954821324",
      "targetHandle": "target",
      "id": "xy-edge__0.6146071780317519source-0.5507247954821324target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.0490499135274598",
      "sourceHandle": "source",
      "target": "0.5507247954821324",
      "targetHandle": "target",
      "id": "xy-edge__0.0490499135274598source-0.5507247954821324target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.1230247439051928",
      "sourceHandle": "source",
      "target": "0.5507247954821324",
      "targetHandle": "target",
      "id": "xy-edge__0.1230247439051928source-0.5507247954821324target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.34302096991368103",
      "sourceHandle": "source",
      "target": "-copy0.23195137482463135",
      "targetHandle": "target",
      "id": "xy-edge__0.34302096991368103source--copy0.23195137482463135target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.09325736548375141",
      "sourceHandle": "source",
      "target": "-copy0.23195137482463135",
      "targetHandle": "target",
      "id": "xy-edge__0.09325736548375141source--copy0.23195137482463135target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.47249815289283914",
      "sourceHandle": "source",
      "target": "0.7032304012631014",
      "targetHandle": "target",
      "id": "xy-edge__0.47249815289283914source-0.7032304012631014target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "9-copy0.9142249922179582",
      "sourceHandle": "source",
      "target": "0.7032304012631014",
      "targetHandle": "target",
      "id": "xy-edge__9-copy0.9142249922179582source-0.7032304012631014target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.48426736445356067",
      "sourceHandle": "source",
      "target": "0.7032304012631014",
      "targetHandle": "target",
      "id": "xy-edge__0.48426736445356067source-0.7032304012631014target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.40552351868555836",
      "sourceHandle": "source",
      "target": "0.47249815289283914",
      "targetHandle": "target",
      "id": "xy-edge__0.40552351868555836source-0.47249815289283914target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.5762349378605824",
      "sourceHandle": "source",
      "target": "9-copy0.9142249922179582",
      "targetHandle": "target",
      "id": "xy-edge__0.5762349378605824source-9-copy0.9142249922179582target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.7617608511325669",
      "sourceHandle": "source",
      "target": "9-copy0.9142249922179582",
      "targetHandle": "target",
      "id": "xy-edge__0.7617608511325669source-9-copy0.9142249922179582target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.0744514779826817",
      "sourceHandle": "source",
      "target": "9-copy0.9142249922179582",
      "targetHandle": "target",
      "id": "xy-edge__0.0744514779826817source-9-copy0.9142249922179582target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "contains",
        "d3f_property": "d3f:contains"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.6146071780317519",
      "sourceHandle": "source",
      "target": "0.1189036182761879",
      "targetHandle": "target",
      "id": "xy-edge__0.6146071780317519source-0.1189036182761879target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "d3f:contains",
        "d3f_property": "d3f:contains"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.1189036182761879",
      "sourceHandle": "source",
      "target": "0.5507247954821324",
      "targetHandle": "target",
      "id": "xy-edge__0.1189036182761879source-0.5507247954821324target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.34945809922391347",
      "sourceHandle": "source",
      "target": "0.40552351868555836",
      "targetHandle": "target",
      "id": "xy-edge__0.34945809922391347source-0.40552351868555836target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.3258831965382004",
      "sourceHandle": "source",
      "target": "0.34945809922391347",
      "targetHandle": "target",
      "id": "xy-edge__0.3258831965382004source-0.34945809922391347target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "analyzes",
        "d3f_property": "analyzes"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.34945809922391347",
      "sourceHandle": "source",
      "target": "0.0490499135274598",
      "targetHandle": "target",
      "id": "xy-edge__0.34945809922391347source-0.0490499135274598target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "analyzes",
        "d3f_property": "analyzes"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.3258831965382004",
      "sourceHandle": "source",
      "target": "0.28963955228702054",
      "targetHandle": "target",
      "id": "xy-edge__0.3258831965382004source-0.28963955228702054target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.9774559813293479",
      "sourceHandle": "source",
      "target": "0.40552351868555836",
      "targetHandle": "target",
      "id": "xy-edge__0.9774559813293479source-0.40552351868555836target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "analyzes",
        "d3f_property": "analyzes"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.9774559813293479",
      "sourceHandle": "source",
      "target": "0.1230247439051928",
      "targetHandle": "target",
      "id": "xy-edge__0.9774559813293479source-0.1230247439051928target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subclassOf",
        "d3f_property": "rdfs:subclassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.2756682259786878",
      "sourceHandle": "source",
      "target": "0.40552351868555836",
      "targetHandle": "target",
      "id": "xy-edge__0.2756682259786878source-0.40552351868555836target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "analyzes",
        "d3f_property": "analyzes"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.2756682259786878",
      "sourceHandle": "source",
      "target": "0.30470669924201865",
      "targetHandle": "target",
      "id": "xy-edge__0.2756682259786878source-0.30470669924201865target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.36833599672722817",
      "sourceHandle": "source",
      "target": "0.40552351868555836",
      "targetHandle": "target",
      "id": "xy-edge__0.36833599672722817source-0.40552351868555836target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.16229972296000217",
      "sourceHandle": "source",
      "target": "0.40552351868555836",
      "targetHandle": "target",
      "id": "xy-edge__0.16229972296000217source-0.40552351868555836target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "analyzes",
        "d3f_property": "analyzes"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.36833599672722817",
      "sourceHandle": "source",
      "target": "0.30470669924201865",
      "targetHandle": "target",
      "id": "xy-edge__0.36833599672722817source-0.30470669924201865target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "analyzes",
        "d3f_property": "analyzes"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.16229972296000217",
      "sourceHandle": "source",
      "target": "0.30470669924201865",
      "targetHandle": "target",
      "id": "xy-edge__0.16229972296000217source-0.30470669924201865target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.9514174898243452",
      "sourceHandle": "source",
      "target": "0.40552351868555836",
      "targetHandle": "target",
      "id": "xy-edge__0.9514174898243452source-0.40552351868555836target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": ":quarantines",
        "d3f_property": ":quarantines"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.48426736445356067",
      "sourceHandle": "source",
      "target": "0.6146071780317519",
      "targetHandle": "target",
      "id": "xy-edge__0.48426736445356067source-0.6146071780317519target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "-copy0.23195137482463135",
      "sourceHandle": "source",
      "target": "0.20366737316992256",
      "targetHandle": "target",
      "id": "xy-edge__-copy0.23195137482463135source-0.20366737316992256target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "verifies",
        "d3f_property": "verifies"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.40552351868555836",
      "sourceHandle": "source",
      "target": "0.1189036182761879",
      "targetHandle": "target",
      "id": "xy-edge__0.40552351868555836source-0.1189036182761879target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "analyzes",
        "d3f_property": "analyzes"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.40552351868555836",
      "sourceHandle": "source",
      "target": "0.5507247954821324",
      "targetHandle": "target",
      "id": "xy-edge__0.40552351868555836source-0.5507247954821324target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "modifies",
        "d3f_property": "modifies"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.5762349378605824",
      "sourceHandle": "source",
      "target": "0.5507247954821324",
      "targetHandle": "target",
      "id": "xy-edge__0.5762349378605824source-0.5507247954821324target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "enforces",
        "d3f_property": "enforces"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.7617608511325669",
      "sourceHandle": "source",
      "target": "0.7314564313202583",
      "targetHandle": "target",
      "id": "xy-edge__0.7617608511325669source-0.7314564313202583target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": ":excises",
        "d3f_property": ":excises"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.7617608511325669",
      "sourceHandle": "source",
      "target": "0.30470669924201865",
      "targetHandle": "target",
      "id": "xy-edge__0.7617608511325669source-0.30470669924201865target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": ":excises",
        "d3f_property": ":excises"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.7617608511325669",
      "sourceHandle": "source",
      "target": "-copy0.23195137482463135",
      "targetHandle": "target",
      "id": "xy-edge__0.7617608511325669source--copy0.23195137482463135target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "enforces",
        "d3f_property": "enforces"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.0744514779826817",
      "sourceHandle": "source",
      "target": "0.7314564313202583",
      "targetHandle": "target",
      "id": "xy-edge__0.0744514779826817source-0.7314564313202583target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "modifies",
        "d3f_property": "modifies"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.7314564313202583",
      "sourceHandle": "source",
      "target": "0.30470669924201865",
      "targetHandle": "target",
      "id": "xy-edge__0.7314564313202583source-0.30470669924201865target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "modifies",
        "d3f_property": "modifies"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.7314564313202583",
      "sourceHandle": "source",
      "target": "-copy0.23195137482463135",
      "targetHandle": "target",
      "id": "xy-edge__0.7314564313202583source--copy0.23195137482463135target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "d3f:may-contain",
        "d3f_property": "d3f:may-contain"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.0490499135274598",
      "sourceHandle": "source",
      "target": "0.9672516677158717",
      "targetHandle": "target",
      "id": "xy-edge__0.0490499135274598source-0.9672516677158717target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.9672516677158717",
      "sourceHandle": "source",
      "target": "-copy0.23195137482463135",
      "targetHandle": "target",
      "id": "xy-edge__0.9672516677158717source--copy0.23195137482463135target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.28963955228702054",
      "sourceHandle": "source",
      "target": "0.9672516677158717",
      "targetHandle": "target",
      "id": "xy-edge__0.28963955228702054source-0.9672516677158717target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.14499280157174388",
      "sourceHandle": "source",
      "target": "0.5507247954821324",
      "targetHandle": "target",
      "id": "xy-edge__0.14499280157174388source-0.5507247954821324target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.16090754731449974",
      "sourceHandle": "source",
      "target": "0.30470669924201865",
      "targetHandle": "target",
      "id": "xy-edge__0.16090754731449974source-0.30470669924201865target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.1189036182761879",
      "sourceHandle": "source",
      "target": "0.16090754731449974",
      "targetHandle": "target",
      "id": "xy-edge__0.1189036182761879source-0.16090754731449974target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "d3f:may-contain",
        "d3f_property": "d3f:may-contain"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.14499280157174388",
      "sourceHandle": "source",
      "target": "0.270595913540307",
      "targetHandle": "target",
      "id": "xy-edge__0.14499280157174388source-0.270595913540307target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.270595913540307",
      "sourceHandle": "source",
      "target": "-copy0.23195137482463135",
      "targetHandle": "target",
      "id": "xy-edge__0.270595913540307source--copy0.23195137482463135target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "d3f:may-contain",
        "d3f_property": "d3f:may-contain"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.14499280157174388",
      "sourceHandle": "source",
      "target": "0.6136178162729569",
      "targetHandle": "target",
      "id": "xy-edge__0.14499280157174388source-0.6136178162729569target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "rdfs:subClassOf",
        "d3f_property": "rdfs:subClassOf"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.6136178162729569",
      "sourceHandle": "source",
      "target": "-copy0.23195137482463135",
      "targetHandle": "target",
      "id": "xy-edge__0.6136178162729569source--copy0.23195137482463135target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "analyzes",
        "d3f_property": "analyzes"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.9514174898243452",
      "sourceHandle": "source",
      "target": "0.5507247954821324",
      "targetHandle": "target",
      "id": "xy-edge__0.9514174898243452source-0.5507247954821324target",
      "selected": false
    },
    {
      "type": "editableEdge",
      "data": {
        "label": "analyzes",
        "d3f_property": "analyzes"
      },
      "markerEnd": {
        "type": "arrowclosed"
      },
      "source": "0.34945809922391347",
      "sourceHandle": "source",
      "target": "0.14499280157174388",
      "targetHandle": "target",
      "id": "xy-edge__0.34945809922391347source-0.14499280157174388target",
      "selected": false
    },
    {
      "source": "0.7752203564382074",
      "sourceHandle": "source",
      "target": "0.1189036182761879",
      "targetHandle": "target",
      "id": "xy-edge__0.7752203564382074source-0.1189036182761879target",
      "selected": false
    }
  ]
};

      const post_cad = (event) => {
        const iframe = document.getElementById("iframe");

        if (event.data?.call === "FromParent") {
          iframe.contentWindow.postMessage(
            {
              call: "toParent",
              value: user_data,
            },
            event.origin
          );
        }
      };

      window.addEventListener("message", (event) => {

        if (event.origin !== "https://next.d3fend.mitre.org") return;

        post_cad(event);
      });
    </script>

    <style>
      #iframe {
        display: block;
        margin: 0 auto;
        width: 100%;
        height: 100vh;
        transform: scale(90%);
        -moz-transform: scale(90%);
        -o-transform: scale(90%);
        -webkit-transform: scale(90%);
      }
    </style>
  </head>

  <main>
    <iframe
      id="iframe"
      src="https://next.d3fend.mitre.org/cad-frame/"
      title="D3FEND CAD Embedded"
    ></iframe>
  </main>
</html>

File Format Verification (d3f:FileFormatVerification) is an important step during Content Validation that safeguards against adversaries masquerading file types (T1036). We wanted to expand on that and provide a few specific techniques to verify file formats with greater technical detail. When researching, we could not find many academic or patent literature from vendor sources in a strict CDR context, but there are published papers related to this in the digital forensic space of file carving. The most common way to verify a file is File Magic Byte Verification (d3f:FileMagicByteVerification), checking that the magic number matches the declared file type. This technique is fundamental in ensuring that files are not misrepresented, which is a common tactic used by adversaries to bypass security measures. The other techniques listed, such as File Entropy Anomaly Detection (d3f:FileEntropyAnomalyDetection), involve more complex procedures. These advanced techniques provide additional layers of security by identifying anomalies that may indicate malicious intent as it is possible for an adversary to spoof the magic number.

## Creating Digital Artifacts

Generating new CDR techniques provided an opportunity to expand the digital artifact ontology. Specifically, while the File (d3f:File) and File Section (d3f:FileSection) artifacts already existed, we've expanded File Section to include the following subclasses to allow more detailed and accurate modeling of file structures: File Header Block (d3f:FileHeaderBlock), File Content Block (d3f:FileContentBlock), and File Footer Block (d3f:FileFooterBlock). The header and footer blocks may contain a signature and additional content, which are types of file metadata; the content block will contain the block's data but may also include some metadata as well, depending on the file format. These artifacts aim to allow any file type to be modeled abstractly. For example, a zip file format can be shown as follows:


With our artifacts, the local file headers and central directory headers are represented by d3f:FileHeaderBlock, where the value of d3f:FileHeaderBlockSignature of the local file headers is 0x504b0304 and the value of the central directory headers is 0x504b0102, according to the zip file format specifications. The data that serve as the data of the zipped files is represented by d3f:FileContentBlockData. Finally, the end of the central directory record is a d3f:FileFooterBlock whose d3f:FileFooterBlockSignature is 0x503b0506. We've provided examples of modeling a PDF and a PE32 file within the notes of the diagram as well.  These examples demonstrate the versatility and applicability of our expanded ontology across different file types and use cases.

## Conclusion

The full, holistic diagram of our CDR work can be found in the CAD diagram below. 

We hope that this blog post shares our insights into our research on CDR techniques and artifacts, as well as provides an introduction to D3FEND's new CAD tool. We believe that this work represents a significant step forward in the understanding and application of CDR technologies. We would love to receive the cybersecurity community's feedback through our GitHub page (XXX). 
