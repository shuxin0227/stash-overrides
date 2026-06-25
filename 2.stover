// Clash Verge 脚本模式
function main(config) {
  // 1. 获取所有节点名称
  const proxyNames = config.proxies.map((p) => p.name);

  // 2. 定义负载均衡组
  const lbGroups = [
    {
      name: "⚖️ 负载均衡-散列",
      type: "load-balance",
      url: "http://www.gstatic.com/generate_204",
      interval: 150,
      strategy: "consistent-hashing",
      proxies: proxyNames,
    },
    {
      name: "⚖️ 负载均衡-轮询",
      type: "load-balance",
      url: "http://www.gstatic.com/generate_204",
      interval: 150,
      strategy: "round-robin",
      proxies: proxyNames,
    }
  ];

  // 3. 将新的负载均衡组插入到 config.proxy-groups 中
  config["proxy-groups"] = [...config["proxy-groups"], ...lbGroups];

  // 4. 将负载均衡组插入到第一个策略组（通常是“节点选择”或“Proxy”）的可选列表中
  // 假设第一个组的索引是 0
  if (config["proxy-groups"].length > 0) {
    config["proxy-groups"][0].proxies.unshift("⚖️ 负载均衡-散列", "⚖️ 负载均衡-轮询");
  }

  return config;
}
