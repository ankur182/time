Step 1. Create the Query object
📁 com.bnpp.asset.v2.domain.facility.queries
Copy code
Java
import lombok.AllArgsConstructor;
import lombok.Getter;

@Getter
@AllArgsConstructor
public class GetAssetsByFacilityIdQuery {
    private final String facilityId;
}
This is just a request model passed through the mediator.
Step 2. Create the Query Handler
📁 com.bnpp.asset.v2.domain.facility.handlers
Copy code
Java
import com.bnpp.asset.v2.domain.facility.queries.GetAssetsByFacilityIdQuery;
import com.bnpp.asset.v2.infrastructure.repositories.SimpleAssetPersistenceRepository;
import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Component;
import java.util.List;

@Component
@RequiredArgsConstructor
public class GetAssetsByFacilityIdHandler implements QueryHandler<GetAssetsByFacilityIdQuery, List<String>> {

    private final SimpleAssetPersistenceRepository simpleAssetPersistenceRepository;

    @Override
    public List<String> handle(GetAssetsByFacilityIdQuery query) {
        return simpleAssetPersistenceRepository.findByFacilityId(query.getFacilityId())
                                               .stream()
                                               .map(asset -> asset.getId().toString())
                                               .toList();
    }
}
✅ This handler takes a facilityId and uses the v2 repository to fetch asset IDs.
It’s your “bridge” between domain service and persistence.
Step 3. Modify your SimpleAssetPersistenceRepository
📁 com.bnpp.asset.v2.infrastructure.repositories
Copy code
Java
import com.bnpp.asset.v2.infrastructure.entities.SimpleAssetEntity;
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;
import java.util.List;

@Repository
public interface SimpleAssetPersistenceRepository extends JpaRepository<SimpleAssetEntity, String> {
    List<SimpleAssetEntity> findByFacilityId(String facilityId);
}
Step 4. Inject the mediator in your service layer
In your FacilityBnppShareService:
Copy code
Java
import com.bnpp.asset.shared.mediator.Mediator; // or similar, depending on your setup

@RequiredArgsConstructor
@Service
public class FacilityBnppShareService {

    private final Mediator mediator;
    // other dependencies...

    private List<String> getAssetIdsForFacility(FacilityBnppShare facilityBnppShare) {
        return mediator.dispatch(new GetAssetsByFacilityIdQuery(facilityBnppShare.getFacilityUniqueId()));
    }
}
