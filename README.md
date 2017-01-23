var nodes = [
    {
        "name": "CLUSTER MID",
        "_id": "ideation_node/47691669357"
    },
    {
        "name": "0a",
        "_id": "ideation_node/47682101101"
    },
    {
        "name": "0b",
        "_id": "ideation_node/47684853613"
    },
    {
        "name": "0",
        "_id": "ideation_node/47681118061"
    },
    {
        "name": "CLUSTER0",
        "_id": "ideation_node/47670959981"
    },
    {
        "name": "CLUSTER1",
        "_id": "ideation_node/47674105709"
    },
    {
        "name": "1a",
        "_id": "ideation_node/47688982381"
    },
    {
        "name": "1",
        "_id": "ideation_node/47686754157"
    }
];

var links = [
    {
        "_from": "ideation_node/47691669357",
        "_to": "ideation_node/47682101101"
    },
    {
        "_from": "ideation_node/47691669357",
        "_to": "ideation_node/47681118061"
    },
    {
        "_from": "ideation_node/47691669357",
        "_to": "ideation_node/47674105709"
    },
    {
        "_from": "ideation_node/47682101101",
        "_to": "ideation_node/47684853613"
    },
    {
        "_from": "ideation_node/47684853613",
        "_to": "ideation_node/47691669357"
    },
    {
        "_from": "ideation_node/47681118061",
        "_to": "ideation_node/47682101101"
    },
    {
        "_from": "ideation_node/47681118061",
        "_to": "ideation_node/47674105709"
    },
    {
        "_from": "ideation_node/47670959981",
        "_to": "ideation_node/47681118061"
    },
    {
        "_from": "ideation_node/47670959981",
        "_to": "ideation_node/47674105709"
    },
    {
        "_from": "ideation_node/47674105709",
        "_to": "ideation_node/47684853613"
    },
    {
        "_from": "ideation_node/47674105709",
        "_to": "ideation_node/47686754157"
    },
    {
        "_from": "ideation_node/47688982381",
        "_to": "ideation_node/47684853613"
    },
    {
        "_from": "ideation_node/47686754157",
        "_to": "ideation_node/47688982381"
    }
];


function getNodeById(nodeId) {
    let nodeToReturn;

    nodes.forEach(node => {
        if (node._id === nodeId) {
            nodeToReturn = node;
            return;
        }
    });

    return nodeToReturn;
}

nodes.forEach(tempNode => {
    tempNode.isVisited = false;
});

function breadthFirstTraverseNodes() {
    let queue = [];
    let rootNode = nodes[0];
    rootNode.isVisited = true;
    queue.push(rootNode);

    while (queue.length > 0) {
        let nextNode = queue[0];
        console.log("=> NEXTNODE", nextNode.name)

        // visit unvisited neighbors
        links.forEach((link, i) => {
            if(i===0){
                console.log("link", link)
            }
            let nodeFrom = getNodeById(link._from);
            // if link._to === nextNode._id then nodeFrom is neighbor, but only queue if nodeFrom has NOT been visited
            if (link._to === nextNode._id && !nodeFrom.isVisited) {
                console.log("nodeFrom", nodeFrom.name, nodeFrom._id)
                nodeFrom.isVisited = true;
                queue.push(nodeFrom);
            }

            // if link._from === nextNode._id then nodeTo is neighbor, but only queue if nodeTo has NOT been visited
            let nodeTo = getNodeById(link._to);
            if (link._from === nextNode._id && !nodeTo.isVisited) {
                console.log("nodeTo", nodeTo.name, nodeTo._id)
                nodeTo.isVisited = true;
                queue.push(nodeTo)
            }

        });
        queue.splice(0, 1);
        console.log("queue", JSON.stringify(queue.map(node => {
            return node.name
        })))
    }
}


breadthFirstTraverseNodes();

