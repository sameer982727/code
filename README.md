// Server.java
import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;
@Document(collection = "servers")
public class Server {
    @Id
    private String id;
    private String name;
    private String language;
    private String framework;
    // getters and setters 
}
// ServerController.java
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;
import java.util.List;
@RestController
@RequestMapping("/api/servers")
public class ServerController {
    private final ServerRepository serverRepository;
    public ServerController(ServerRepository serverRepository) {
        this.serverRepository = serverRepository;
    }
    @GetMapping
    public List<Server> getAllServers() {
        return serverRepository.findAll();
    }
    @GetMapping("/{id}")
    public Server getServerById(@PathVariable String id) {
        return serverRepository.findById(id).orElse(null);
    }
    @PostMapping
    public Server createServer(@RequestBody Server server) {
        return serverRepository.save(server);
    }
    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteServer(@PathVariable String id) {
        serverRepository.deleteById(id);
        return ResponseEntity.noContent().build();
    }
}
