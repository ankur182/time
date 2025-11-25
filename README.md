package com.bnpp.asset.v2.domain.models.projectfinance;

import com.bnpp.asset.v2.domain.models.Page;
import com.bnpp.asset.v2.domain.models.Pageable;
import java.util.List;

public class PageProjectFinance implements Page<ProjectFinance> {

    private final List<ProjectFinance> content;
    private final Pageable pageable;

    public PageProjectFinance(List<ProjectFinance> content, Pageable pageable) {
        this.content = content;
        this.pageable = pageable;
    }

    @Override
    public List<ProjectFinance> getContent() {
        return content;
    }

    @Override
    public Pageable getPageable() {
        return pageable;
    }
}
