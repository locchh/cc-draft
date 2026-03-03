# AWS AI Agent Services

## AWS Bedrock

Foundational Models Provider Service of AWS support:

1. Wide range of Foundational Models (Nova, Claude, Mistral, Llama, Huggingface, etc.)

2. Infer (Single Prompt, Chat, Text, Image, etc.)

3. Token Count

4. Tuning (Custom model, Prompt routing, etc.)

5. Build:
    
    5.1 Agent
    
    5.2 Flow (Connect Amazon Bedrock Prompts, Agents, Knowledge Base, Guardrails and other AWS services to create, test 
    and deploy user-defined generative AI workflows.)
    
    5.3 Knowledge Base (Amazon Bedrock Knowledge Bases provides fully managed support for end-to-end RAG workflow.)
    
    5.4 Guardrails
    
    5.5 Prompt Management
    
    5.6 Data Automation (Bedrock Data Automation (BDA) enables you to automate the generation of valuable insights from unstructured multimodal content such as documents, images, video, and audio to build generative AI)
    
    5.7 Agentcore

6. Assets

7. Optimation
    7.1 Prompt Caching
    7.2 Prompt Routing

## Strands Agents

Strands Agents offers a framework for developing and testing agents, working seamlessly with any model, including those from Anthropic and OpenAI. Including:

1. Building

2. Safety and Security

3. Observability and Debugging

4. Evaluation

5. Deploy

## AWS Agentcore

AgentCore is an agentic platform for building, deploying, and operating effective agents securely at scale.

### 1. Agentcore Runtime

AgentCore Runtime is a secure, serverless runtime purpose-built for deploying and scaling dynamic AI agents and tools. Deploy your agents in seconds with direct code upload or choose container deployment for advanced configurations and maximum flexibility.

- Create the agent
- Test locally
- Configure for deployment
- Deploy to AWS
- Invoke the live agent

### 2. Agentcore Gateways

AgentCore Gateway is an Agentcore sub-service that enables agents to securely access tools by transforming APIs and Lambda functions into agent-compatible tools and connecting to existing MCP servers. Related to `bedrock-agentcore-starter-toolkit`.

### 3. Agentcore Memory

AgentCore Memory is an Agentcore sub-service that makes it easy for developers to build context-aware agents by eliminating complex memory infrastructure management while providing complete control over what the agent remembers and learns.

### 4. Agentcore Identity

AgentCore Identity is an Agentcore sub-service that allows your agents to securely access and operate across AWS resources or third-party tools and services, on behalf of users or by themselves, with scoped permissions, delegated access, and identity-aware authorization.

### 5. Agentcore Observability

AgentCore Observability is a managed service that delivers comprehensive operational insights to trace, debug, and monitor AI agent performance, providing real-time visibility into agent workflows with OpenTelemetry-compatible integration.

### 6. Agentcore Policy

Policy in Amazon Bedrock AgentCore helps ensure agents stay within defined boundaries without slowing them down. Policy integrates with AgentCore Gateway to intercept every tool call in real time, ensuring agents stay within defined boundaries without slowing them down.

### 7. Agentcore Built-in tools

AgentCore Code Interpreter enables agents to write and execute code securely in sandbox environments, enhancing their accuracy and expanding their ability to solve complex end-to-end tasks.

AgentCore Browser provides a fast, secure, cloud-based browser runtime that enables agents to interact with websites and carry out web-based workflows at scale with reduced CAPTCHA interruptions.

### 8. Agentcore Evaluation

AgentCore Evaluations helps teams improve agent performance in production through continuous performance monitoring and real-time quality scoring. The service automatically samples and scores live interactions using 13 built-in evaluators.

## References

- [AWS Bedrock Demonstration](https://bedrock-demonstration.marketing.aws.dev/?refid=1f887566-8561-4bf2-a30b-f383e290b094)

- [AWS Bedrock Getting Started](https://docs.aws.amazon.com/bedrock/latest/userguide/getting-started.html)

- [AWS AgentCore Presentation](https://bedrock-demonstration.marketing.aws.dev/agent-core)

- [AWS AgentCore Getting Started](https://docs.aws.amazon.com/bedrock-agentcore/latest/devguide/agentcore-get-started-toolkit.html)

- [AWS AgentCore Pricing](https://aws.amazon.com/bedrock/agentcore/pricing/)

- [Strands Agents Documentation](https://strandsagents.com/latest/documentation/docs/)

- [Amazon Bedrock Workshop](https://github.com/aws-samples/amazon-bedrock-workshop)

- [AWS AgentCore Samples](https://github.com/awslabs/amazon-bedrock-agentcore-samples)

- [Amazon Bedrock Agent Samples](https://github.com/awslabs/amazon-bedrock-agent-samples)