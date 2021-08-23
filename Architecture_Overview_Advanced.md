```mermaid
%% =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
%% Newforma Architecture Overview (advanced) 
%% To test, use Chrome Extension: https://chrome.google.com/webstore/detail/markdown-diagrams/pmoglnmodacnbbofbgcagndelmgaclel
%% =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
flowchart LR

    subgraph Microsoft
        PersonalAccount(Personal Account)
        AuthFlow(Authentication Flow)
        AzureAD(AzureAD)
        subgraph MSServices
            GraphAPI(Graph API)
            AzureADApp(Azure AD Application)
        end
        subgraph MSApps
            Office365(Office 365)
            Exchange(Exchange)
            OneDrive(OneDrive)
            SharePoint(SharePoint)
        end
    end

    subgraph Partners
        Procore(Procore) --> Ryvit(Ryvit)
    end

    subgraph Users
        Outlook(fa:fa-envelope Outlook Addin)
        Android(fa:fa-android Android)
        iOS(fa:fa-apple iOS)
        Web(fa:fa-chrome Web)
    end

    subgraph AWS
        subgraph APIs
            api[/api.newforma.cloud/]
            eapi[/enterprise.api.newforma.cloud/]
            npcapi[/npcapi.newforma.cloud/]
        end
        subgraph Compute
            Lambda{fa:fa-amazon Lambda}
            ECS{ECS}
            EC2{EC2}
        end
        subgraph Storage
            S3[(S3)]
        end
        subgraph Networking & Content Delivery
            API_Gateway>API Gateway]
            Cloudfront>Cloudfront]
            VPC>VPC]
        end
        subgraph Security, Identity & Compliance
            Cognito(Cognito)
            IAM(IAM)
            KMS(KMS)
        end
        subgraph Database
            DynamoDB[(DynamoDB)]
            Aurora[(Aurora)]
            Elastisearch[(Elastisearch)]
            Kinesis[(Kinesis)]
        end
        subgraph Management & Governance
            CloudFormation(CloudFormation)
            CloudWatch(CloudWatch)
            CloudTrail(CloudTrail)
            OpsWork(OpsWork)
        end
    end

    subgraph CorporateNetwork
        ADFS(ADFS)
        AzureADAppProxy(Azure AD Application Proxy Connectors)
        subgraph NewformaConnectors
            NewformaLink(NewformaLink)
            NewformaApi(NewformaApi)
        end
        NIX(InfoExchange)
        NPCS(NPCS)
        MySQL[(MySQL)]
    end
    
    %% Draw connections
    NIX-->NPCS
    NPCS-->MySQL
    AWS-->GraphAPI
    AWS-->AzureADApp
    AzureADApp-->AzureADAppProxy
    AzureADAppProxy-->NewformaLink
    AzureADAppProxy-->NewformaApi
    AuthFlow-->AzureAD
    AuthFlow-->PersonalAccount
    NewformaConnectors-->MySQL
    Users-->AuthFlow
    AzureAD-->ADFS  

    %% Draw dotted connections
    Partners-.->eapi
    Users-.->api
    NPCS-.->npcapi

    %% CSS modifications
    classDef green fill:#9d6,stroke:#333,stroke-width:2px
    classDef orange fill:#eb9,stroke:#333,stroke-width:6px
    classDef blue fill:#aae,stroke:#468,stroke-width:8px
    class Users,Partners,CorporateNetwork,Microsoft blue
    class api,eapi,npcapi green
    class AWS orange
```
